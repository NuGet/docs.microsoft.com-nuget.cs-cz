---
title: "Poznámky k verzi NuGet 2.1 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6f972803-9e17-43f5-b77b-973c3accf695
description: "Poznámky k verzi pro NuGet 2.1 včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 2.1 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: dafe575eedbfed215c0b1c86795bea281de97252
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="50e17-104">Poznámky k verzi 2.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="50e17-104">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="50e17-105">[Poznámky k verzi NuGet 2.0](../release-notes/nuget-2.0.md) | [NuGet 2.2 poznámky k verzi](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="50e17-105">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="50e17-106">4. října 2012 byla vydána NuGet 2.1.</span><span class="sxs-lookup"><span data-stu-id="50e17-106">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="50e17-107">Hierarchická soubor nuget.config.</span><span class="sxs-lookup"><span data-stu-id="50e17-107">Hierarchical Nuget.Config</span></span>
<span data-ttu-id="50e17-108">NuGet 2.1 vám dává větší flexibilitu při řízení nastavení NuGet prostřednictvím rekurzivně proti si strukturu složek hledání `NuGet.Config` soubory a pak vytváření konfigurace ze sady všech nalezených souborů.</span><span class="sxs-lookup"><span data-stu-id="50e17-108">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="50e17-109">Jako příklad vezměte v úvahu scénář, kde má tým úložiště interní balíčků pro položky konfigurace sestavení z jiných vnitřní závislosti.</span><span class="sxs-lookup"><span data-stu-id="50e17-109">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="50e17-110">Struktura složek pro jednotlivé projekt může vypadat následovně:</span><span class="sxs-lookup"><span data-stu-id="50e17-110">The folder structure for an individual project might look like the following:</span></span>

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

<span data-ttu-id="50e17-111">Kromě toho pokud obnovení balíčku je povolená pro řešení, do následující složky budou existovat také:</span><span class="sxs-lookup"><span data-stu-id="50e17-111">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

    C:\myteam\solution1\.nuget

<span data-ttu-id="50e17-112">Aby bylo možné používat úložiště na interní balíčků tým služby, které jsou k dispozici pro všechny projekty, které tým funguje, při není ji dáte k dispozici pro každý projekt na počítači, můžeme vytvoření nového souboru Nuget.Config a umístěte jej do složky c:\myteam.</span><span class="sxs-lookup"><span data-stu-id="50e17-112">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="50e17-113">Neexistuje žádný způsob, jak na určením složku balíčků pro projekt.</span><span class="sxs-lookup"><span data-stu-id="50e17-113">There is no way to specificy a packages folder per project.</span></span>

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="50e17-114">Teď vidíme, že byl přidán zdroj spuštěním příkazu 'nuget.exe zdroje' z libovolné složky pod c:\myteam jak je uvedeno níže:</span><span class="sxs-lookup"><span data-stu-id="50e17-114">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Zdroje balíčků z konfigurace nadřazené nuget](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="50e17-116">`NuGet.Config`soubory jsou vyhledávány v následujícím pořadí:</span><span class="sxs-lookup"><span data-stu-id="50e17-116">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="50e17-117">Provede rekurzivní ze složky projektu kořenovou</span><span class="sxs-lookup"><span data-stu-id="50e17-117">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="50e17-118">Globální `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span><span class="sxs-lookup"><span data-stu-id="50e17-118">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="50e17-119">Tyto konfigurace se než použijí v *pořadí*, znamená to, že je založeno na výše uvedené pořadí, globální Nuget.Config by se použije první, následuje zjištěných Nuget.Config soubory z kořenové složky projektu, a potom podle `.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="50e17-119">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="50e17-120">To je zvlášť důležité, pokud používáte `<clear/>` elementu, který chcete odebrat sadu položek z konfigurace.</span><span class="sxs-lookup"><span data-stu-id="50e17-120">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="50e17-121">Zadejte umístění složky ' balíčky.</span><span class="sxs-lookup"><span data-stu-id="50e17-121">Specify ‘packages’ Folder Location</span></span>
<span data-ttu-id="50e17-122">V minulosti má NuGet spravované balíčků řešení ze složky známé, balíčky, nalezeno pod kořenové složky řešení.</span><span class="sxs-lookup"><span data-stu-id="50e17-122">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="50e17-123">Pro vývojové týmy, které mají mnoho různých řešení, které mají nainstalované balíčky NuGet to může způsobit ve stejném balíčku instaluje na mnoha různých místech v systému souborů.</span><span class="sxs-lookup"><span data-stu-id="50e17-123">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="50e17-124">NuGet 2.1 poskytuje podrobnější kontrolu nad umístění složky balíčky prostřednictvím `repositoryPath` element v `NuGet.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="50e17-124">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="50e17-125">Vytváření v předchozím příkladu hierarchické Nuget.Config podpory, předpokládá, že chceme mít všechny projekty v části C:\myteam\ sdílet stejnou složku balíčků.</span><span class="sxs-lookup"><span data-stu-id="50e17-125">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="50e17-126">K tomu jednoduše přidejte následující položku na `c:\myteam\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="50e17-126">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="50e17-127">V tomto příkladu sdílený `Nuget.Config` soubor Určuje balíčky sdílené složky pro každý projekt, který se vytvoří pod C:\myteam, bez ohledu na to hloubka.</span><span class="sxs-lookup"><span data-stu-id="50e17-127">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="50e17-128">Poznámka: Pokud máte existující balíčky složce pod kořenového adresáře řešení, bude muset odstranit před NuGet umístí balíčky v novém umístění.</span><span class="sxs-lookup"><span data-stu-id="50e17-128">Note that if you have an existing packages folder underneath your solution root, you will need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="50e17-129">Podpora pro přenosné knihovny</span><span class="sxs-lookup"><span data-stu-id="50e17-129">Support for Portable Libraries</span></span>
<span data-ttu-id="50e17-130">[Přenosné knihovny](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) je funkce poprvé .NET 4, který vám umožní sestavovat sestavení, které můžete pracovat bez úprav na různých platformách Microsoft, z verzí rozhraní.NET Framework pro Silverlight pro Windows Phone a i Xbox 360 (i když v současné době nepodporuje NuGet cíl přenosné knihovny Xbox).</span><span class="sxs-lookup"><span data-stu-id="50e17-130">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="50e17-131">Tím, že rozšíří [balíček konvence](../create-packages/supporting-multiple-target-frameworks.md) profilů a framework verze NuGet 2.1 teď podporuje přenosné knihovny tím, že vám vytvořit balíčky, které mají složené framework a profil cíle `lib` složek.</span><span class="sxs-lookup"><span data-stu-id="50e17-131">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="50e17-132">Jako příklad zvažte následující knihovny přenosných tříd dostupných cílových platforem.</span><span class="sxs-lookup"><span data-stu-id="50e17-132">As an example, consider the following portable class library’s available target platforms.</span></span>

![Dialogové okno Vytvoření přenosné knihovny](./media/releasenotes-21-plib.png)

<span data-ttu-id="50e17-134">Jakmile je vytvořen knihovny a příkaz `nuget.exe pack MyPortableProject.csproj` běží, nové přenositelností struktura složek balíček knihovny můžete zobrazit tak, že prověří obsah vygenerovaný balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="50e17-134">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Přenosná knihovna balíček rozložení](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="50e17-136">Jak vidíte, konvence název složky přenosné knihovny se následující 'přenosné-{framework 1} + {framework n}' kde identifikátory framework podle existující [framework název a verze konvence](../schema/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="50e17-136">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../schema/target-frameworks.md).</span></span> <span data-ttu-id="50e17-137">Jedinou výjimkou konvence název a verzi nachází v identifikátoru framework se používá pro Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="50e17-137">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="50e17-138">Tato Přezdívka měli použít název rozhraní "wp" (wp7, wp71 nebo wp8).</span><span class="sxs-lookup"><span data-stu-id="50e17-138">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="50e17-139">Pomocí "silverlight-wp7", například bude výsledkem chyba.</span><span class="sxs-lookup"><span data-stu-id="50e17-139">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="50e17-140">Při instalaci balíčku, který je vytvořený z této struktura složek, NuGet nyní pravidla můžete použít jeho framework a profil pro více cílů, jako je zadaný v názvu složky.</span><span class="sxs-lookup"><span data-stu-id="50e17-140">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="50e17-141">Za pravidel porovnávání NuGet je Princip "konkrétnější" cíle má přednost před "méně specifických".</span><span class="sxs-lookup"><span data-stu-id="50e17-141">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="50e17-142">To znamená, že monikery cílení na konkrétní platformu vždy upřednostňované přes přenosné ty Pokud jsou oba kompatibilní s projektem.</span><span class="sxs-lookup"><span data-stu-id="50e17-142">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="50e17-143">Kromě toho pokud víc přenosného cíle jsou kompatibilní s projektem, NuGet přednost jeden, kde je "nejbližší" do projektu balíček odkazování na sadu platformy podporované.</span><span class="sxs-lookup"><span data-stu-id="50e17-143">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="50e17-144">Cílení Windows 8 a Windows Phone 8 projekty</span><span class="sxs-lookup"><span data-stu-id="50e17-144">Targeting Windows 8 and Windows Phone 8 Projects</span></span>
<span data-ttu-id="50e17-145">Kromě přidání podpory pro cílení na přenosné knihovny projekty, NuGet 2.1 poskytuje nové monikery framework pro projekty úložiště systému Windows 8 a Windows Phone 8, jakož i některé nové obecné zástupných názvů pro Windows Store a Windows Phone projekty, které budou snazší správa v budoucích verzích příslušné platformy.</span><span class="sxs-lookup"><span data-stu-id="50e17-145">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="50e17-146">Pro aplikace pro Windows 8 Store identifikátory vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="50e17-146">For Windows 8 Store applications, the identifiers look as follows:</span></span>

|<span data-ttu-id="50e17-147">NuGet 2.0 a starší</span><span class="sxs-lookup"><span data-stu-id="50e17-147">NuGet 2.0 and earlier</span></span>|<span data-ttu-id="50e17-148">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="50e17-148">NuGet 2.1</span></span>|
|----------------|-----------|
|<span data-ttu-id="50e17-149">winRT45. NETCore45</span><span class="sxs-lookup"><span data-stu-id="50e17-149">winRT45, .NETCore45</span></span>|<span data-ttu-id="50e17-150">Windows, Windows8, win, win8</span><span class="sxs-lookup"><span data-stu-id="50e17-150">Windows, Windows8, win, win8</span></span>|

<br/>
<span data-ttu-id="50e17-151">Pro projekty Windows Phone identifikátorů vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="50e17-151">For Windows Phone projects, the identifiers look as follows:</span></span>

|<span data-ttu-id="50e17-152">Phone OS</span><span class="sxs-lookup"><span data-stu-id="50e17-152">Phone OS</span></span>|<span data-ttu-id="50e17-153">NuGet 2.0 a starší</span><span class="sxs-lookup"><span data-stu-id="50e17-153">NuGet 2.0 and earlier</span></span>|<span data-ttu-id="50e17-154">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="50e17-154">NuGet 2.1</span></span>
|----------------|-----------|-----------|
|<span data-ttu-id="50e17-155">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="50e17-155">Windows Phone 7</span></span>|<span data-ttu-id="50e17-156">silverlight3 wp</span><span class="sxs-lookup"><span data-stu-id="50e17-156">silverlight3-wp</span></span>|<span data-ttu-id="50e17-157">webové části, WindowsPhone7 wp7, WindowsPhone,</span><span class="sxs-lookup"><span data-stu-id="50e17-157">wp, wp7, WindowsPhone, WindowsPhone7</span></span>|
|<span data-ttu-id="50e17-158">Windows Phone 7.5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="50e17-158">Windows Phone 7.5 (Mango)</span></span>|<span data-ttu-id="50e17-159">silverilght4 wp71</span><span class="sxs-lookup"><span data-stu-id="50e17-159">silverilght4-wp71</span></span>|<span data-ttu-id="50e17-160">wp71 WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="50e17-160">wp71, WindowsPhone71</span></span>|
|<span data-ttu-id="50e17-161">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="50e17-161">Windows Phone 8</span></span>|<span data-ttu-id="50e17-162">(není podporována)</span><span class="sxs-lookup"><span data-stu-id="50e17-162">(not supported)</span></span>|<span data-ttu-id="50e17-163">wp8 WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="50e17-163">wp8, WindowsPhone8</span></span>|
<br/>
<span data-ttu-id="50e17-164">Ve všech výše uvedených změny budou nadále původní názvy framework plně podporovat NuGet 2.1.</span><span class="sxs-lookup"><span data-stu-id="50e17-164">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="50e17-165">Klouzavý dopředu, nové názvy je třeba použít jak budou stabilnější v budoucích verzích příslušné platformy.</span><span class="sxs-lookup"><span data-stu-id="50e17-165">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="50e17-166">Nové názvy bude *není* se nepodporuje ve verzích NuGet před 2.1, ale, takže podle toho naplánovat pro případ, aby přepínač.</span><span class="sxs-lookup"><span data-stu-id="50e17-166">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="50e17-167">Vylepšené vyhledávání v dialogovém okně Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="50e17-167">Improved Search in Package Manager Dialog</span></span>
<span data-ttu-id="50e17-168">Změny byly zavedeny v posledních několika iterací, do Galerie NuGet, který výrazně Vylepšená rychlost a relevance balíček hledání.</span><span class="sxs-lookup"><span data-stu-id="50e17-168">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="50e17-169">Tato vylepšení byly však omezeny na nuget.org Web.</span><span class="sxs-lookup"><span data-stu-id="50e17-169">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="50e17-170">NuGet 2.1 zpřístupňuje vylepšené vyhledávání prostředí prostřednictvím dialogové okno Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="50e17-170">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="50e17-171">Jako příklad Představte si, že jste chtěli najít balíček Windows Azure ukládání do mezipaměti Preview.</span><span class="sxs-lookup"><span data-stu-id="50e17-171">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="50e17-172">Přiměřené vyhledávací dotaz pro tento balíček může být "Azure Cache".</span><span class="sxs-lookup"><span data-stu-id="50e17-172">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="50e17-173">V předchozích verzích dialogové okno Správce balíčku nebude požadovaný balíček uvedený i na první stránce výsledků.</span><span class="sxs-lookup"><span data-stu-id="50e17-173">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="50e17-174">Ale v NuGet 2.1 požadované balíčku se zobrazí v horní části výsledků vyhledávání.</span><span class="sxs-lookup"><span data-stu-id="50e17-174">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Balíček správce dialogové okno hledání](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="50e17-176">Vynucení aktualizace balíčku</span><span class="sxs-lookup"><span data-stu-id="50e17-176">Force Package Update</span></span>
<span data-ttu-id="50e17-177">Před 2.1 NuGet, které by NuGet přeskočit aktualizace balíčku, pokud došlo není číslo vysoké verze.</span><span class="sxs-lookup"><span data-stu-id="50e17-177">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="50e17-178">To se zavedl třecí pro určité scénáře – zejména v případě sestavení nebo CI scénáře, kde týmem nechtěli se zvýší číslo s každé sestavení verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="50e17-178">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="50e17-179">Toto chování žádoucí bylo vynutit aktualizaci bez ohledu na to.</span><span class="sxs-lookup"><span data-stu-id="50e17-179">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="50e17-180">NuGet 2.1 řeší to s příznakem 'přeinstalujte'.</span><span class="sxs-lookup"><span data-stu-id="50e17-180">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="50e17-181">Předchozí verze NuGet například by způsobilo následující při pokusu o aktualizaci balíčku, který neměl novější verze balíčku:</span><span class="sxs-lookup"><span data-stu-id="50e17-181">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

<span data-ttu-id="50e17-182">S příznakem přeinstalovat, bude aktualizován balíček bez ohledu na to, jestli existuje novější verze.</span><span class="sxs-lookup"><span data-stu-id="50e17-182">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

<span data-ttu-id="50e17-183">Jiné scénáře, kde prokáže výhodné příznak přeinstalovat je, že znovu cílových framework.</span><span class="sxs-lookup"><span data-stu-id="50e17-183">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="50e17-184">Při změně cílový framework projektu (například z .NET 4 na rozhraní .NET 4.5), balíček aktualizace-přeinstalujte můžete aktualizovat odkazy na správné sestavení pro všechny balíčky NuGet, které jsou nainstalované v projektu.</span><span class="sxs-lookup"><span data-stu-id="50e17-184">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="50e17-185">Upravit zdroje balíčků ve Visual Studiu</span><span class="sxs-lookup"><span data-stu-id="50e17-185">Edit Package Sources Within Visual Studio</span></span>
<span data-ttu-id="50e17-186">V předchozích verzích NuGet aktualizace zdroj balíčku z v rámci dialogové okno Možnosti sady Visual Studio vyžaduje odstranění a znovu přidat zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="50e17-186">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="50e17-187">Podpora aktualizace jako první třídy funkce uživatelského rozhraní pro konfiguraci zlepšuje NuGet 2.1 Tento pracovní postup.</span><span class="sxs-lookup"><span data-stu-id="50e17-187">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Dialogové okno Konfigurace správce balíčku](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="50e17-189">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="50e17-189">Bug Fixes</span></span>
<span data-ttu-id="50e17-190">NuGet 2.1 obsahuje opravy mnoha chyb.</span><span class="sxs-lookup"><span data-stu-id="50e17-190">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="50e17-191">Úplný seznam pracovní položky pevná ve NuGet 2.0, prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="50e17-191">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
