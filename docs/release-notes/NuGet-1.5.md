---
title: Poznámky k verzi 1.5 verzi NuGet
description: Poznámky k verzi pro NuGet 1.5 včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1f2f7ebe718ce943faa31b7e19395eead8726648
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821340"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="29b8d-103">Poznámky k verzi 1.5 verzi NuGet</span><span class="sxs-lookup"><span data-stu-id="29b8d-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="29b8d-104">[Poznámky k verzi NuGet 1.4](../release-notes/nuget-1.4.md) | [NuGet 1.6 poznámky k verzi](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="29b8d-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="29b8d-105">NuGet 1.5 byla vydána 30 Srpen 2011.</span><span class="sxs-lookup"><span data-stu-id="29b8d-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="29b8d-106">Funkce</span><span class="sxs-lookup"><span data-stu-id="29b8d-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="29b8d-107">Šablony projektů s předinstalovanými NuGet balíčky</span><span class="sxs-lookup"><span data-stu-id="29b8d-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="29b8d-108">Při vytváření nové šablony projektu ASP.NET MVC 3, knihovny skriptů jQuery zahrnutý v projektu ve skutečnosti tam umístili instalace balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="29b8d-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="29b8d-109">Šablona projektu ASP.NET MVC 3 zahrnuje sadu balíčky NuGet, které budou instalovány při vyvolání šablona projektu.</span><span class="sxs-lookup"><span data-stu-id="29b8d-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="29b8d-110">Tato schopnost mezi ně patřit balíčky NuGet pomocí šablony projektu je nyní funkce NuGet, _žádné_ šablona projektu teď můžete využít výhod.</span><span class="sxs-lookup"><span data-stu-id="29b8d-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="29b8d-111">Další podrobnosti o této funkci najdete v tématu to [příspěvku na blogu vývojáře funkce](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="29b8d-111">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="29b8d-112">Odkazy na explicitní sestavení</span><span class="sxs-lookup"><span data-stu-id="29b8d-112">Explicit Assembly References</span></span>

<span data-ttu-id="29b8d-113">Přidat novou `<references />` elementu použitého k explicitnímu zadání sestavení, v rámci na balíček by měl odkazovat.</span><span class="sxs-lookup"><span data-stu-id="29b8d-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="29b8d-114">Například přidejte následující:</span><span class="sxs-lookup"><span data-stu-id="29b8d-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="29b8d-115">Pak pouze `xunit.dll` a `xunit.extensions.dll` se bude odkazovat z příslušné [framework nebo profilu podsložky](../reference/nuspec.md#explicit-assembly-references) z `lib` složky, i když existují další sestavení ve složce.</span><span class="sxs-lookup"><span data-stu-id="29b8d-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="29b8d-116">Pokud tento element je tento parametr vynechán, pak platí obvyklé chování, která má odkazovat na všechna sestavení v `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="29b8d-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="29b8d-117">__Co se tato funkce používá?__</span><span class="sxs-lookup"><span data-stu-id="29b8d-117">__What is this feature used for?__</span></span>

<span data-ttu-id="29b8d-118">Tato funkce podporuje pouze sestavení v době návrhu.</span><span class="sxs-lookup"><span data-stu-id="29b8d-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="29b8d-119">Například při použití kontrakty kódu, kontrakt sestavení musí být vedle sestavení modulu runtime, která budou posílení, aby Visual Studio můžete je vyhledat, ale sestavení smlouvy nesmí odkazovat ve skutečnosti projektu a nesmí být zkopírován do `bin` složky.</span><span class="sxs-lookup"><span data-stu-id="29b8d-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="29b8d-120">Podobně tato funkce slouží k pro systémů testů jednotek, jako je například XUnit, které musí jeho nástroje pro sestavení vedle sestavení za běhu, ale vyloučené z odkazů projektu.</span><span class="sxs-lookup"><span data-stu-id="29b8d-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="29b8d-121">Přidání možnosti vyloučit soubory ve příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="29b8d-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="29b8d-122">`<file>` v rámci `.nuspec` soubor lze použít k zahrnutí konkrétní soubor nebo sadu souborů pomocí zástupného znaku.</span><span class="sxs-lookup"><span data-stu-id="29b8d-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="29b8d-123">Pokud používáte zástupný znak, neexistuje žádný způsob, jak vyloučit určitou podmnožinu zahrnuté soubory.</span><span class="sxs-lookup"><span data-stu-id="29b8d-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="29b8d-124">Předpokládejme například, že chcete všechny textových souborů ve složce s výjimkou některou.</span><span class="sxs-lookup"><span data-stu-id="29b8d-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="29b8d-125">Chcete-li zadat více souborů použijte středníky.</span><span class="sxs-lookup"><span data-stu-id="29b8d-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="29b8d-126">Nebo vyloučit určitou sadu souborů, jako je například všechny záložní soubory použít zástupný znak</span><span class="sxs-lookup"><span data-stu-id="29b8d-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="29b8d-127">Odebrání balíčků v dialogovém okně zobrazí výzvu k odebrání závislostí</span><span class="sxs-lookup"><span data-stu-id="29b8d-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="29b8d-128">Při odinstalaci balíčku se závislostmi, NuGet vyzve, povolení odebrání závislostí balíčků balíčku společně s.</span><span class="sxs-lookup"><span data-stu-id="29b8d-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Odebrání závislých balíčků](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="29b8d-130">`Get-Package` příkaz zlepšování</span><span class="sxs-lookup"><span data-stu-id="29b8d-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="29b8d-131">`Get-Package` Příkaz teď podporuje `-ProjectName` parametr.</span><span class="sxs-lookup"><span data-stu-id="29b8d-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="29b8d-132">Takže příkaz</span><span class="sxs-lookup"><span data-stu-id="29b8d-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="29b8d-133">Zobrazí seznam všech balíčky nainstalované v projektu A.</span><span class="sxs-lookup"><span data-stu-id="29b8d-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="29b8d-134">Podpora pro proxy servery, které vyžadují ověřování</span><span class="sxs-lookup"><span data-stu-id="29b8d-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="29b8d-135">Při použití NuGet za proxy server, který vyžaduje ověření, výzvou k zadání přihlašovacích údajů proxy teď NuGet.</span><span class="sxs-lookup"><span data-stu-id="29b8d-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="29b8d-136">Zadání přihlašovacích údajů umožňuje NuGet pro připojení k Vzdálené úložiště.</span><span class="sxs-lookup"><span data-stu-id="29b8d-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="29b8d-137">Podpora pro úložiště, které vyžadují ověřování</span><span class="sxs-lookup"><span data-stu-id="29b8d-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="29b8d-138">NuGet teď podporuje připojení k [privátní úložiště](../hosting-packages/local-feeds.md) základní ověřování nebo ověřování NTLM, které vyžadují.</span><span class="sxs-lookup"><span data-stu-id="29b8d-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="29b8d-139">Podpora pro ověřování hodnotou hash bude přidán v budoucí verzi.</span><span class="sxs-lookup"><span data-stu-id="29b8d-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="29b8d-140">Vylepšení výkonu do úložiště nuget.org</span><span class="sxs-lookup"><span data-stu-id="29b8d-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="29b8d-141">Provedli jsme několik vylepšení výkonu do Galerie nuget.org do balíček výpis a rychlejší hledání.</span><span class="sxs-lookup"><span data-stu-id="29b8d-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="29b8d-142">Řešení dialogovém okně projekt filtrování</span><span class="sxs-lookup"><span data-stu-id="29b8d-142">Solution dialog project filtering</span></span>
<span data-ttu-id="29b8d-143">V dialogu úrovni řešení při zobrazení výzvy ke jaké projekty k instalaci ukážeme pouze projekty, které jsou kompatibilní s vybraným balíčkem.</span><span class="sxs-lookup"><span data-stu-id="29b8d-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="29b8d-144">Poznámky k verzi balíčku</span><span class="sxs-lookup"><span data-stu-id="29b8d-144">Package Release Notes</span></span>
<span data-ttu-id="29b8d-145">Balíčky NuGet nyní zahrnují podporu pro poznámky k verzi.</span><span class="sxs-lookup"><span data-stu-id="29b8d-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="29b8d-146">Poznámky k verzi jenom zobrazit si při prohlížení _aktualizace_ pro balíček, takže nemá smysl chcete přidat do první verzi.</span><span class="sxs-lookup"><span data-stu-id="29b8d-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Poznámky k verzi v rámci kartu aktualizace](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="29b8d-148">Chcete-li přidat poznámky k verzi balíčku, použijte nové `<releaseNotes />` element metadata v souboru NuSpec.</span><span class="sxs-lookup"><span data-stu-id="29b8d-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="29b8d-149">příponou .nuspec & ltfiles /&gt; zlepšování</span><span class="sxs-lookup"><span data-stu-id="29b8d-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="29b8d-150">`.nuspec` Souboru teď umožňuje prázdný `<files />` element, který sděluje nuget.exe nechcete zahrnout všechny soubory v balíčku.</span><span class="sxs-lookup"><span data-stu-id="29b8d-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="29b8d-151">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="29b8d-151">Bug Fixes</span></span>
<span data-ttu-id="29b8d-152">NuGet 1.5 měl celkem 107 pracovní položky, které jsou pevné.</span><span class="sxs-lookup"><span data-stu-id="29b8d-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="29b8d-153">103 těchto byly označeny jako chyby.</span><span class="sxs-lookup"><span data-stu-id="29b8d-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="29b8d-154">Úplný seznam pracovní položky pevná ve NuGet 1.5 prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="29b8d-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="29b8d-155">Opravy chyb vhodné poznamenat:</span><span class="sxs-lookup"><span data-stu-id="29b8d-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="29b8d-156">[Problém 1273](http://nuget.codeplex.com/workitem/1273): provedené `packages.config` více verzí popisný abecedně řazení balíčky a odebrání navíc mezer.</span><span class="sxs-lookup"><span data-stu-id="29b8d-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="29b8d-157">[Problém 844](http://nuget.codeplex.com/workitem/844): čísla verzí jsou nyní normalized tak, aby `Install-Package 1.0` funguje na balíček s verzí `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="29b8d-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="29b8d-158">[Problém 1060](http://nuget.codeplex.com/workitem/1060): při vytváření balíčku pomocí nuget.exe, `-Version` příznak přepsání `<version />` elementu.</span><span class="sxs-lookup"><span data-stu-id="29b8d-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>