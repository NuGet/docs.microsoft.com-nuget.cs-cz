---
title: Poznámky k verzi 1.5 NuGet
description: Zpráva k vydání verze pro NuGet 1.5, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548722"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="40675-103">Poznámky k verzi 1.5 NuGet</span><span class="sxs-lookup"><span data-stu-id="40675-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="40675-104">[Zpráva k vydání verze NuGet 1.4](../release-notes/nuget-1.4.md) | [zpráva k vydání verze NuGet 1.6](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="40675-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="40675-105">NuGet 1.5 vydané 30. srpna 2011.</span><span class="sxs-lookup"><span data-stu-id="40675-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="40675-106">Funkce</span><span class="sxs-lookup"><span data-stu-id="40675-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="40675-107">Šablony projektů s předinstalovanou NuGet balíčky</span><span class="sxs-lookup"><span data-stu-id="40675-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="40675-108">Při vytváření nové šablony projektu ASP.NET MVC 3, knihovny skriptů jQuery zahrnutý v projektu jsou ve skutečnosti tam umístili instalace balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="40675-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="40675-109">Šablona projektu ASP.NET MVC 3 zahrnuje sadu balíčků NuGet, které se nainstalují při vyvolání šablony projektu.</span><span class="sxs-lookup"><span data-stu-id="40675-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="40675-110">Tato možnost zahrnout balíčky NuGet pomocí šablony projektu je teď součástí balíčku nuget, který _jakékoli_ šablony projektu můžete nově využít výhod.</span><span class="sxs-lookup"><span data-stu-id="40675-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="40675-111">Další podrobnosti o této funkci najdete v tomto [příspěvek na blogu od vývojářů funkci](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="40675-111">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="40675-112">Odkazy na explicitní sestavení</span><span class="sxs-lookup"><span data-stu-id="40675-112">Explicit Assembly References</span></span>

<span data-ttu-id="40675-113">Přidat nový `<references />` použít k explicitnímu zadání sestavení, v rámci elementu balíček by se měla odkazovat.</span><span class="sxs-lookup"><span data-stu-id="40675-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="40675-114">Například přidejte následující:</span><span class="sxs-lookup"><span data-stu-id="40675-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="40675-115">Pak jenom `xunit.dll` a `xunit.extensions.dll` bude odkazovat z příslušné [framework nebo profil podsložky](../reference/nuspec.md#explicit-assembly-references) z `lib` složky, i když existují jiné sestavení ve složce.</span><span class="sxs-lookup"><span data-stu-id="40675-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="40675-116">Pokud tento prvek je vynechán, pak platí obvyklé chování, která má odkazovat na všechna sestavení v `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="40675-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="40675-117">__Co tato funkce slouží?__</span><span class="sxs-lookup"><span data-stu-id="40675-117">__What is this feature used for?__</span></span>

<span data-ttu-id="40675-118">Tato funkce podporuje jenom sestavení doby návrhu.</span><span class="sxs-lookup"><span data-stu-id="40675-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="40675-119">Například při použití kontrakty kódu, sestavení kontraktu musí být vedle sestavení modulu runtime, které se rozšiřují, aby sada Visual Studio můžete najít je, ale sestavení kontraktu nesmí odkazovat ve skutečnosti projekt a by neměl být zkopírována do `bin` složky.</span><span class="sxs-lookup"><span data-stu-id="40675-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="40675-120">Podobně tato funkce umožňuje pro rozhraní pro testování částí jako jsou XUnit, které potřebují jeho nástroje pro sestavení vedle sestavení modulu runtime, ale vyloučit z projektových odkazů.</span><span class="sxs-lookup"><span data-stu-id="40675-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="40675-121">Přidání možnosti vyloučit soubory souboru .nuspec</span><span class="sxs-lookup"><span data-stu-id="40675-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="40675-122">`<file>` v elementu `.nuspec` souboru je možné zahrnout určitý soubor nebo sady souborů pomocí zástupného znaku.</span><span class="sxs-lookup"><span data-stu-id="40675-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="40675-123">Při použití zástupného znaku, neexistuje žádný způsob, jak vyloučit určitou podmnožinu zahrnuté soubory.</span><span class="sxs-lookup"><span data-stu-id="40675-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="40675-124">Předpokládejme například, že chcete všechny textové soubory ve složce s výjimkou konkrétní skupinu.</span><span class="sxs-lookup"><span data-stu-id="40675-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="40675-125">Chcete-li zadat více souborů použijte středníky.</span><span class="sxs-lookup"><span data-stu-id="40675-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="40675-126">Nebo použijte zástupný znak pro vyloučení sadu souborů, jako jsou všechny záložní soubory</span><span class="sxs-lookup"><span data-stu-id="40675-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="40675-127">Odebrání balíčků v dialogovém okně zobrazí výzvu k odebrání závislostí</span><span class="sxs-lookup"><span data-stu-id="40675-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="40675-128">Při odinstalaci balíčku se závislostmi, vyzve NuGet umožňuje odebrání závislosti balíčku společně s balíček.</span><span class="sxs-lookup"><span data-stu-id="40675-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Odebrání závislé balíčky](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="40675-130">`Get-Package` zlepšení příkazu</span><span class="sxs-lookup"><span data-stu-id="40675-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="40675-131">`Get-Package` Příkaz nyní podporuje `-ProjectName` parametru.</span><span class="sxs-lookup"><span data-stu-id="40675-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="40675-132">Takže příkaz</span><span class="sxs-lookup"><span data-stu-id="40675-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="40675-133">Zobrazí seznam všech balíčků nainstalovaných ve projekt A.</span><span class="sxs-lookup"><span data-stu-id="40675-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="40675-134">Podpora pro proxy servery, které vyžadují ověřování</span><span class="sxs-lookup"><span data-stu-id="40675-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="40675-135">Pokud používáte NuGet za proxy serverem, který vyžaduje ověření, NuGet teď zadání přihlašovacích údajů proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="40675-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="40675-136">Zadání přihlašovacích údajů umožňuje NuGet pro připojení k Vzdálené úložiště.</span><span class="sxs-lookup"><span data-stu-id="40675-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="40675-137">Podpora pro úložiště, které vyžadují ověřování</span><span class="sxs-lookup"><span data-stu-id="40675-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="40675-138">NuGet teď podporuje připojení k [soukromých úložišť](../hosting-packages/local-feeds.md) , které vyžadují základní ověřování nebo ověřování NTLM.</span><span class="sxs-lookup"><span data-stu-id="40675-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="40675-139">Podpora pro ověřování algoritmem Digest bude přidána v budoucí verzi.</span><span class="sxs-lookup"><span data-stu-id="40675-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="40675-140">Vylepšení výkonu pro úložiště nuget.org</span><span class="sxs-lookup"><span data-stu-id="40675-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="40675-141">Provedli jsme několik vylepšení výkonu v galerii nuget.org na balíček výpis a rychlejší hledání.</span><span class="sxs-lookup"><span data-stu-id="40675-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="40675-142">Filtrování řešení dialogové okno projektu</span><span class="sxs-lookup"><span data-stu-id="40675-142">Solution dialog project filtering</span></span>
<span data-ttu-id="40675-143">V okně úrovni řešení při zobrazení výzvy ke jaké projekty k instalaci ukážeme pouze projekty, které jsou kompatibilní s vybraným balíčkem.</span><span class="sxs-lookup"><span data-stu-id="40675-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="40675-144">Zpráva k vydání verze balíčku</span><span class="sxs-lookup"><span data-stu-id="40675-144">Package Release Notes</span></span>
<span data-ttu-id="40675-145">Balíčky NuGet nyní zahrnují podporu pro zprávu k vydání verze.</span><span class="sxs-lookup"><span data-stu-id="40675-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="40675-146">Poznámky k verzi zobrazit pouze až při zobrazení _aktualizace_ balíčku, proto nemá smysl přidat do vaší první verze.</span><span class="sxs-lookup"><span data-stu-id="40675-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Zpráva k vydání verze v rámci kartu aktualizace](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="40675-148">Chcete-li přidat poznámky k verzi balíčku, použijte nové `<releaseNotes />` prvek metadat v souboru NuSpec.</span><span class="sxs-lookup"><span data-stu-id="40675-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="40675-149">souboru .nuspec & ltfiles /&gt; zlepšení</span><span class="sxs-lookup"><span data-stu-id="40675-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="40675-150">`.nuspec` Souboru teď umožňuje prázdný `<files />` element, který informuje nuget.exe nechcete zahrnout všechny soubory v balíčku.</span><span class="sxs-lookup"><span data-stu-id="40675-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="40675-151">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="40675-151">Bug Fixes</span></span>
<span data-ttu-id="40675-152">NuGet 1.5 bylo celkem 107 pracovní položky opraveno.</span><span class="sxs-lookup"><span data-stu-id="40675-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="40675-153">103 z nich byly označeny jako chyby.</span><span class="sxs-lookup"><span data-stu-id="40675-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="40675-154">Úplný seznam pracovních položek opravených NuGet 1.5 prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="40675-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="40675-155">Opravy chyb za zmínku:</span><span class="sxs-lookup"><span data-stu-id="40675-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="40675-156">[Problém 1273](http://nuget.codeplex.com/workitem/1273): provedené `packages.config` více verzí popisný řazení balíčky podle abecedy a odebráním prázdné znaky.</span><span class="sxs-lookup"><span data-stu-id="40675-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="40675-157">[Problém 844](http://nuget.codeplex.com/workitem/844): čísla verzí se nyní normalizují tak, aby `Install-Package 1.0` funguje na balíček s verzí `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="40675-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="40675-158">[Problém 1060](http://nuget.codeplex.com/workitem/1060): při vytváření balíčku pomocí nuget.exe, `-Version` příznak přepsání `<version />` elementu.</span><span class="sxs-lookup"><span data-stu-id="40675-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
