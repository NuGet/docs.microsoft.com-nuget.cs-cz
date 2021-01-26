---
title: Zpráva k vydání verze NuGet 1,5
description: Poznámky k verzi pro NuGet 1,5, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c9946f3d8cf545ec14f842c40105743c231b4b72
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777099"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="cda21-103">Zpráva k vydání verze NuGet 1,5</span><span class="sxs-lookup"><span data-stu-id="cda21-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="cda21-104">Zpráva k [vydání verze](../release-notes/nuget-1.4.md)  |  NuGet 1,4 Zpráva k [vydání verze NuGet 1,6](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="cda21-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="cda21-105">NuGet 1,5 byl vydán 30. srpna 2011.</span><span class="sxs-lookup"><span data-stu-id="cda21-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="cda21-106">Funkce</span><span class="sxs-lookup"><span data-stu-id="cda21-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="cda21-107">Šablony projektů s předinstalovanými balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="cda21-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="cda21-108">Při vytváření nové šablony projektu ASP.NET MVC 3 se ve vlastně umístění knihoven skriptů jQuery obsažených v projektu nainstalují balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="cda21-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="cda21-109">Šablona projektu ASP.NET MVC 3 obsahuje sadu balíčků NuGet, které se instalují při vyvolání šablony projektu.</span><span class="sxs-lookup"><span data-stu-id="cda21-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="cda21-110">Tato možnost zahrnout balíčky NuGet se šablonou projektu je teď funkcí NuGet, kterou může mít _každá_ šablona projektu teď možnost využít.</span><span class="sxs-lookup"><span data-stu-id="cda21-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="cda21-111">Další podrobnosti o této funkci najdete [v tomto blogovém příspěvku vývojářem této funkce](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="cda21-111">For more details about this feature, read this [blog post by the developer of the feature](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="cda21-112">Explicitní odkazy na sestavení</span><span class="sxs-lookup"><span data-stu-id="cda21-112">Explicit Assembly References</span></span>

<span data-ttu-id="cda21-113">Přidání nového `<references />` elementu, který slouží k explicitnímu určení sestavení, která mají být v rámci balíčku odkazována.</span><span class="sxs-lookup"><span data-stu-id="cda21-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="cda21-114">Například pokud přidáte následující:</span><span class="sxs-lookup"><span data-stu-id="cda21-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="cda21-115">Pak bude `xunit.dll` odkazována pouze na a `xunit.extensions.dll` z příslušné [podsložky architektury nebo profilu](../reference/nuspec.md#explicit-assembly-references) ve složce, `lib` i když jsou ve složce jiná sestavení.</span><span class="sxs-lookup"><span data-stu-id="cda21-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="cda21-116">Pokud je tento element vynechán, použije se obvyklé chování, které má odkazovat na každé sestavení ve `lib` složce.</span><span class="sxs-lookup"><span data-stu-id="cda21-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="cda21-117">__K čemu se tato funkce používá?__</span><span class="sxs-lookup"><span data-stu-id="cda21-117">__What is this feature used for?__</span></span>

<span data-ttu-id="cda21-118">Tato funkce podporuje sestavení pouze pro dobu návrhu.</span><span class="sxs-lookup"><span data-stu-id="cda21-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="cda21-119">Například při použití kontraktů kódu musí být sestavení kontraktu vedle sestavení modulu runtime, která rozšiřují, aby je Visual Studio mohl najít, ale sestavení kontraktu by na ně neměla odkazovat v projektu a neměla by být kopírována do `bin` složky.</span><span class="sxs-lookup"><span data-stu-id="cda21-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="cda21-120">Podobně lze funkci použít pro rozhraní testování částí, jako je například XUnit, které vyžadují, aby jejich nástroje byly umístěny vedle sestavení modulu runtime, ale vyloučeny z odkazů na projekt.</span><span class="sxs-lookup"><span data-stu-id="cda21-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="cda21-121">Přidání možnosti pro vyloučení souborů v souboru. nuspec</span><span class="sxs-lookup"><span data-stu-id="cda21-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="cda21-122">`<file>`Element v `.nuspec` souboru lze použít k zahrnutí konkrétního souboru nebo sady souborů pomocí zástupného znaku.</span><span class="sxs-lookup"><span data-stu-id="cda21-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="cda21-123">Pokud používáte zástupný znak, neexistuje žádný způsob, jak vyloučit určitou podmnožinu zahrnutých souborů.</span><span class="sxs-lookup"><span data-stu-id="cda21-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="cda21-124">Předpokládejme například, že chcete všechny textové soubory ve složce s výjimkou konkrétního.</span><span class="sxs-lookup"><span data-stu-id="cda21-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="cda21-125">K určení více souborů použijte středníky.</span><span class="sxs-lookup"><span data-stu-id="cda21-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="cda21-126">Případně můžete použít zástupnou kartu k vyloučení sady souborů, například všech záložních souborů.</span><span class="sxs-lookup"><span data-stu-id="cda21-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="cda21-127">Odebrání balíčků pomocí dialogových oken pro odebrání závislostí</span><span class="sxs-lookup"><span data-stu-id="cda21-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="cda21-128">Při odinstalaci balíčku se závislostmi se zobrazí výzva NuGet umožňující odebrání závislostí balíčku spolu s balíčkem.</span><span class="sxs-lookup"><span data-stu-id="cda21-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Odebírají se závislé balíčky.](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="cda21-130">`Get-Package` vylepšení příkazu</span><span class="sxs-lookup"><span data-stu-id="cda21-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="cda21-131">`Get-Package`Příkaz teď podporuje `-ProjectName` parametr.</span><span class="sxs-lookup"><span data-stu-id="cda21-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="cda21-132">Příkaz</span><span class="sxs-lookup"><span data-stu-id="cda21-132">So the command</span></span>

```
Get-Package –ProjectName A
```

<span data-ttu-id="cda21-133">Zobrazí seznam všech balíčků nainstalovaných v projektu A.</span><span class="sxs-lookup"><span data-stu-id="cda21-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="cda21-134">Podpora proxy serverů, které vyžadují ověření</span><span class="sxs-lookup"><span data-stu-id="cda21-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="cda21-135">Při používání NuGet za proxy serverem, který vyžaduje ověření, NuGet se teď vyzve k zadání přihlašovacích údajů proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="cda21-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="cda21-136">Zadání přihlašovacích údajů umožňuje NuGet připojit se ke vzdálenému úložišti.</span><span class="sxs-lookup"><span data-stu-id="cda21-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="cda21-137">Podpora úložišť, která vyžadují ověření</span><span class="sxs-lookup"><span data-stu-id="cda21-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="cda21-138">NuGet teď podporuje připojení k [soukromým úložištím](../hosting-packages/local-feeds.md) , která vyžadují základní ověřování nebo ověřování NTLM.</span><span class="sxs-lookup"><span data-stu-id="cda21-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="cda21-139">V budoucí verzi se přidá podpora pro ověřování algoritmem Digest.</span><span class="sxs-lookup"><span data-stu-id="cda21-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="cda21-140">Vylepšení výkonu úložiště nuget.org</span><span class="sxs-lookup"><span data-stu-id="cda21-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="cda21-141">V galerii nuget.org jsme provedli několik vylepšení výkonu, aby se vytvářely výpisy balíčků a hledání rychleji.</span><span class="sxs-lookup"><span data-stu-id="cda21-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="cda21-142">Filtrování projektu dialogu řešení</span><span class="sxs-lookup"><span data-stu-id="cda21-142">Solution dialog project filtering</span></span>
<span data-ttu-id="cda21-143">V dialogovém okně na úrovni řešení se po zobrazení výzvy k instalaci projektů zobrazí pouze projekty, které jsou kompatibilní s vybraným balíčkem.</span><span class="sxs-lookup"><span data-stu-id="cda21-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="cda21-144">Poznámky k verzi balíčku</span><span class="sxs-lookup"><span data-stu-id="cda21-144">Package Release Notes</span></span>
<span data-ttu-id="cda21-145">Balíčky NuGet teď zahrnují podporu pro poznámky k verzi.</span><span class="sxs-lookup"><span data-stu-id="cda21-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="cda21-146">Poznámky k verzi se zobrazují jenom při prohlížení _aktualizací_ balíčku, takže nedávají smysl přidat ho do vaší první verze.</span><span class="sxs-lookup"><span data-stu-id="cda21-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Poznámky k verzi na kartě aktualizace](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="cda21-148">Chcete-li přidat do balíčku poznámky k verzi, použijte nový `<releaseNotes />` prvek metadat v souboru NuSpec.</span><span class="sxs-lookup"><span data-stu-id="cda21-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="cda21-149">. nuspec &ltfiles/ &gt; vylepšení</span><span class="sxs-lookup"><span data-stu-id="cda21-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="cda21-150">`.nuspec`Soubor teď umožňuje prázdný `<files />` element, který oznamuje nuget.exe nezahrnovat do balíčku žádný soubor.</span><span class="sxs-lookup"><span data-stu-id="cda21-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="cda21-151">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="cda21-151">Bug Fixes</span></span>
<span data-ttu-id="cda21-152">Aktualizace NuGet 1,5 obsahovala celkem 107 pracovních položek.</span><span class="sxs-lookup"><span data-stu-id="cda21-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="cda21-153">103 z nich bylo označeno jako chyby.</span><span class="sxs-lookup"><span data-stu-id="cda21-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="cda21-154">Úplný seznam pracovních položek opravených v NuGet 1,5 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="cda21-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="cda21-155">Opravy chyb zaznamenaly:</span><span class="sxs-lookup"><span data-stu-id="cda21-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="cda21-156">[Problém 1273](http://nuget.codeplex.com/workitem/1273): provedli jsme `packages.config` lepší řízení verzí pomocí řazení balíčků abecedně a odebráním nadbytečného prázdného znaku.</span><span class="sxs-lookup"><span data-stu-id="cda21-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="cda21-157">[Problém 844](http://nuget.codeplex.com/workitem/844): čísla verzí jsou nyní normalizována, aby `Install-Package 1.0` fungovala na balíčku s verzí `1.0.0` .</span><span class="sxs-lookup"><span data-stu-id="cda21-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="cda21-158">[Problém 1060](http://nuget.codeplex.com/workitem/1060): při vytváření balíčku pomocí nuget.exe `-Version` příznak Přepisuje `<version />` prvek.</span><span class="sxs-lookup"><span data-stu-id="cda21-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
