---
title: Poznámky k verzi 2.1 NuGet
description: Poznámky k verzi pro NuGet 2.1 včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3b7a000098a7362f4b1c2c4072c6cd1468baf9b5
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="c6e45-103">Poznámky k verzi 2.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="c6e45-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="c6e45-104">[Poznámky k verzi NuGet 2.0](../release-notes/nuget-2.0.md) | [NuGet 2.2 poznámky k verzi](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="c6e45-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="c6e45-105">4. října 2012 byla vydána NuGet 2.1.</span><span class="sxs-lookup"><span data-stu-id="c6e45-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="c6e45-106">Hierarchická soubor nuget.config.</span><span class="sxs-lookup"><span data-stu-id="c6e45-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="c6e45-107">NuGet 2.1 vám dává větší flexibilitu při řízení nastavení NuGet prostřednictvím rekurzivně proti si strukturu složek hledání `NuGet.Config` soubory a pak vytváření konfigurace ze sady všech nalezených souborů.</span><span class="sxs-lookup"><span data-stu-id="c6e45-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="c6e45-108">Jako příklad vezměte v úvahu scénář, kde má tým úložiště interní balíčků pro položky konfigurace sestavení z jiných vnitřní závislosti.</span><span class="sxs-lookup"><span data-stu-id="c6e45-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="c6e45-109">Struktura složek pro jednotlivé projekt může vypadat následovně:</span><span class="sxs-lookup"><span data-stu-id="c6e45-109">The folder structure for an individual project might look like the following:</span></span>

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

<span data-ttu-id="c6e45-110">Kromě toho pokud obnovení balíčku je povolená pro řešení, do následující složky budou existovat také:</span><span class="sxs-lookup"><span data-stu-id="c6e45-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

    C:\myteam\solution1\.nuget

<span data-ttu-id="c6e45-111">Aby bylo možné používat úložiště na interní balíčků tým služby, které jsou k dispozici pro všechny projekty, které tým funguje, při není ji dáte k dispozici pro každý projekt na počítači, můžeme vytvoření nového souboru Nuget.Config a umístěte jej do složky c:\myteam.</span><span class="sxs-lookup"><span data-stu-id="c6e45-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="c6e45-112">Neexistuje žádný způsob, jak na určením složku balíčků pro projekt.</span><span class="sxs-lookup"><span data-stu-id="c6e45-112">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="c6e45-113">Teď vidíme, že byl přidán zdroj spuštěním příkazu 'nuget.exe zdroje' z libovolné složky pod c:\myteam jak je uvedeno níže:</span><span class="sxs-lookup"><span data-stu-id="c6e45-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Zdroje balíčků z konfigurace nadřazené nuget](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="c6e45-115">`NuGet.Config` soubory jsou vyhledávány v následujícím pořadí:</span><span class="sxs-lookup"><span data-stu-id="c6e45-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="c6e45-116">Provede rekurzivní ze složky projektu kořenovou</span><span class="sxs-lookup"><span data-stu-id="c6e45-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="c6e45-117">Globální `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span><span class="sxs-lookup"><span data-stu-id="c6e45-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="c6e45-118">Tyto konfigurace se než použijí v *pořadí*, znamená to, že je založeno na výše uvedené pořadí, globální Nuget.Config by se použije první, následuje zjištěných Nuget.Config soubory z kořenové složky projektu, a potom podle `.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="c6e45-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="c6e45-119">To je zvlášť důležité, pokud používáte `<clear/>` elementu, který chcete odebrat sadu položek z konfigurace.</span><span class="sxs-lookup"><span data-stu-id="c6e45-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="c6e45-120">Zadejte umístění složky ' balíčky.</span><span class="sxs-lookup"><span data-stu-id="c6e45-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="c6e45-121">V minulosti má NuGet spravované balíčků řešení ze složky známé, balíčky, nalezeno pod kořenové složky řešení.</span><span class="sxs-lookup"><span data-stu-id="c6e45-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="c6e45-122">Pro vývojové týmy, které mají mnoho různých řešení, které mají nainstalované balíčky NuGet to může způsobit ve stejném balíčku instaluje na mnoha různých místech v systému souborů.</span><span class="sxs-lookup"><span data-stu-id="c6e45-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="c6e45-123">NuGet 2.1 poskytuje podrobnější kontrolu nad umístění složky balíčky prostřednictvím `repositoryPath` element v `NuGet.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="c6e45-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="c6e45-124">Vytváření v předchozím příkladu hierarchické Nuget.Config podpory, předpokládá, že chceme mít všechny projekty v části C:\myteam\ sdílet stejnou složku balíčků.</span><span class="sxs-lookup"><span data-stu-id="c6e45-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="c6e45-125">K tomu jednoduše přidejte následující položku na `c:\myteam\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="c6e45-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="c6e45-126">V tomto příkladu sdílený `Nuget.Config` soubor Určuje balíčky sdílené složky pro každý projekt, který se vytvoří pod C:\myteam, bez ohledu na to hloubka.</span><span class="sxs-lookup"><span data-stu-id="c6e45-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="c6e45-127">Poznámka: Pokud máte existující balíčky složce pod kořenového adresáře řešení, budete muset odstranit před NuGet umístí balíčky v novém umístění.</span><span class="sxs-lookup"><span data-stu-id="c6e45-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="c6e45-128">Podpora pro přenosné knihovny</span><span class="sxs-lookup"><span data-stu-id="c6e45-128">Support for Portable Libraries</span></span>

<span data-ttu-id="c6e45-129">[Přenosné knihovny](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) je funkce poprvé .NET 4, který vám umožní sestavovat sestavení, které můžete pracovat bez úprav na různých platformách Microsoft, z verzí rozhraní.NET Framework pro Silverlight pro Windows Phone a i Xbox 360 (i když v současné době nepodporuje NuGet cíl přenosné knihovny Xbox).</span><span class="sxs-lookup"><span data-stu-id="c6e45-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="c6e45-130">Tím, že rozšíří [balíček konvence](../create-packages/supporting-multiple-target-frameworks.md) profilů a framework verze NuGet 2.1 teď podporuje přenosné knihovny tím, že vám vytvořit balíčky, které mají složené framework a profil cíle `lib` složek.</span><span class="sxs-lookup"><span data-stu-id="c6e45-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="c6e45-131">Jako příklad zvažte následující knihovny přenosných tříd dostupných cílových platforem.</span><span class="sxs-lookup"><span data-stu-id="c6e45-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Dialogové okno Vytvoření přenosné knihovny](./media/releasenotes-21-plib.png)

<span data-ttu-id="c6e45-133">Jakmile je vytvořen knihovny a příkaz `nuget.exe pack MyPortableProject.csproj` běží, nové přenositelností struktura složek balíček knihovny můžete zobrazit tak, že prověří obsah vygenerovaný balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="c6e45-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Přenosná knihovna balíček rozložení](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="c6e45-135">Jak vidíte, konvence název složky přenosné knihovny se následující 'přenosné-{framework 1} + {framework n}' kde identifikátory framework podle existující [framework název a verze konvence](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="c6e45-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="c6e45-136">Jedinou výjimkou konvence název a verzi nachází v identifikátoru framework se používá pro Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="c6e45-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="c6e45-137">Tato Přezdívka měli použít název rozhraní "wp" (wp7, wp71 nebo wp8).</span><span class="sxs-lookup"><span data-stu-id="c6e45-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="c6e45-138">Pomocí "silverlight-wp7", například bude výsledkem chyba.</span><span class="sxs-lookup"><span data-stu-id="c6e45-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="c6e45-139">Při instalaci balíčku, který je vytvořený z této struktura složek, NuGet nyní pravidla můžete použít jeho framework a profil pro více cílů, jako je zadaný v názvu složky.</span><span class="sxs-lookup"><span data-stu-id="c6e45-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="c6e45-140">Za pravidel porovnávání NuGet je Princip "konkrétnější" cíle má přednost před "méně specifických".</span><span class="sxs-lookup"><span data-stu-id="c6e45-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="c6e45-141">To znamená, že monikery cílení na konkrétní platformu vždy upřednostňované přes přenosné ty Pokud jsou oba kompatibilní s projektem.</span><span class="sxs-lookup"><span data-stu-id="c6e45-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="c6e45-142">Kromě toho pokud víc přenosného cíle jsou kompatibilní s projektem, NuGet přednost jeden, kde je "nejbližší" do projektu balíček odkazování na sadu platformy podporované.</span><span class="sxs-lookup"><span data-stu-id="c6e45-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="c6e45-143">Cílení Windows 8 a Windows Phone 8 projekty</span><span class="sxs-lookup"><span data-stu-id="c6e45-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="c6e45-144">Kromě přidání podpory pro cílení na přenosné knihovny projekty, NuGet 2.1 poskytuje nové monikery framework pro projekty úložiště systému Windows 8 a Windows Phone 8, jakož i některé nové obecné zástupných názvů pro Windows Store a Windows Phone projekty, které budou snazší správa v budoucích verzích příslušné platformy.</span><span class="sxs-lookup"><span data-stu-id="c6e45-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="c6e45-145">Pro aplikace pro Windows 8 Store identifikátory vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="c6e45-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="c6e45-146">NuGet 2.0 a starší</span><span class="sxs-lookup"><span data-stu-id="c6e45-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="c6e45-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="c6e45-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="c6e45-148">winRT45, .NETCore45</span><span class="sxs-lookup"><span data-stu-id="c6e45-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="c6e45-149">Windows, Windows8, win, win8</span><span class="sxs-lookup"><span data-stu-id="c6e45-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="c6e45-150">Pro projekty Windows Phone identifikátorů vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="c6e45-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="c6e45-151">Phone OS</span><span class="sxs-lookup"><span data-stu-id="c6e45-151">Phone OS</span></span> | <span data-ttu-id="c6e45-152">NuGet 2.0 a starší</span><span class="sxs-lookup"><span data-stu-id="c6e45-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="c6e45-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="c6e45-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6e45-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="c6e45-154">Windows Phone 7</span></span> | <span data-ttu-id="c6e45-155">silverlight3-wp</span><span class="sxs-lookup"><span data-stu-id="c6e45-155">silverlight3-wp</span></span> | <span data-ttu-id="c6e45-156">webové části, WindowsPhone7 wp7, WindowsPhone,</span><span class="sxs-lookup"><span data-stu-id="c6e45-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="c6e45-157">Windows Phone 7.5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="c6e45-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="c6e45-158">silverlight4 wp71</span><span class="sxs-lookup"><span data-stu-id="c6e45-158">silverlight4-wp71</span></span> | <span data-ttu-id="c6e45-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="c6e45-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="c6e45-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="c6e45-160">Windows Phone 8</span></span> | <span data-ttu-id="c6e45-161">(není podporována)</span><span class="sxs-lookup"><span data-stu-id="c6e45-161">(not supported)</span></span> | <span data-ttu-id="c6e45-162">wp8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="c6e45-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="c6e45-163">Ve všech výše uvedených změny budou nadále původní názvy framework plně podporovat NuGet 2.1.</span><span class="sxs-lookup"><span data-stu-id="c6e45-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="c6e45-164">Klouzavý dopředu, nové názvy je třeba použít jak budou stabilnější v budoucích verzích příslušné platformy.</span><span class="sxs-lookup"><span data-stu-id="c6e45-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="c6e45-165">Nové názvy bude *není* se nepodporuje ve verzích NuGet před 2.1, ale, takže podle toho naplánovat pro případ, aby přepínač.</span><span class="sxs-lookup"><span data-stu-id="c6e45-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="c6e45-166">Vylepšené vyhledávání v dialogovém okně Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="c6e45-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="c6e45-167">Změny byly zavedeny v posledních několika iterací, do Galerie NuGet, který výrazně Vylepšená rychlost a relevance balíček hledání.</span><span class="sxs-lookup"><span data-stu-id="c6e45-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="c6e45-168">Tato vylepšení byly však omezeny na nuget.org Web.</span><span class="sxs-lookup"><span data-stu-id="c6e45-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="c6e45-169">NuGet 2.1 zpřístupňuje vylepšené vyhledávání prostředí prostřednictvím dialogové okno Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="c6e45-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="c6e45-170">Jako příklad Představte si, že jste chtěli najít balíček Windows Azure ukládání do mezipaměti Preview.</span><span class="sxs-lookup"><span data-stu-id="c6e45-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="c6e45-171">Přiměřené vyhledávací dotaz pro tento balíček může být "Azure Cache".</span><span class="sxs-lookup"><span data-stu-id="c6e45-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="c6e45-172">V předchozích verzích dialogové okno Správce balíčku nebude požadovaný balíček uvedený i na první stránce výsledků.</span><span class="sxs-lookup"><span data-stu-id="c6e45-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="c6e45-173">Ale v NuGet 2.1 požadované balíčku se zobrazí v horní části výsledků vyhledávání.</span><span class="sxs-lookup"><span data-stu-id="c6e45-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Balíček správce dialogové okno hledání](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="c6e45-175">Vynucení aktualizace balíčku</span><span class="sxs-lookup"><span data-stu-id="c6e45-175">Force Package Update</span></span>

<span data-ttu-id="c6e45-176">Před 2.1 NuGet, které by NuGet přeskočit aktualizace balíčku, pokud došlo není číslo vysoké verze.</span><span class="sxs-lookup"><span data-stu-id="c6e45-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="c6e45-177">To se zavedl třecí pro určité scénáře – zejména v případě sestavení nebo CI scénáře, kde týmem nechtěli se zvýší číslo s každé sestavení verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="c6e45-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="c6e45-178">Toto chování žádoucí bylo vynutit aktualizaci bez ohledu na to.</span><span class="sxs-lookup"><span data-stu-id="c6e45-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="c6e45-179">NuGet 2.1 řeší to s příznakem 'přeinstalujte'.</span><span class="sxs-lookup"><span data-stu-id="c6e45-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="c6e45-180">Předchozí verze NuGet například by způsobilo následující při pokusu o aktualizaci balíčku, který neměl novější verze balíčku:</span><span class="sxs-lookup"><span data-stu-id="c6e45-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

<span data-ttu-id="c6e45-181">S příznakem přeinstalovat, bude aktualizován balíček bez ohledu na to, jestli existuje novější verze.</span><span class="sxs-lookup"><span data-stu-id="c6e45-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

<span data-ttu-id="c6e45-182">Jiné scénáře, kde prokáže výhodné příznak přeinstalovat je, že znovu cílových framework.</span><span class="sxs-lookup"><span data-stu-id="c6e45-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="c6e45-183">Při změně cílový framework projektu (například z .NET 4 na rozhraní .NET 4.5), balíček aktualizace-přeinstalujte můžete aktualizovat odkazy na správné sestavení pro všechny balíčky NuGet, které jsou nainstalované v projektu.</span><span class="sxs-lookup"><span data-stu-id="c6e45-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="c6e45-184">Upravit zdroje balíčků ve Visual Studiu</span><span class="sxs-lookup"><span data-stu-id="c6e45-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="c6e45-185">V předchozích verzích NuGet aktualizace zdroj balíčku z v rámci dialogové okno Možnosti sady Visual Studio vyžaduje odstranění a znovu přidat zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="c6e45-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="c6e45-186">Podpora aktualizace jako první třídy funkce uživatelského rozhraní pro konfiguraci zlepšuje NuGet 2.1 Tento pracovní postup.</span><span class="sxs-lookup"><span data-stu-id="c6e45-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Dialogové okno Konfigurace správce balíčku](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="c6e45-188">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="c6e45-188">Bug Fixes</span></span>

<span data-ttu-id="c6e45-189">NuGet 2.1 obsahuje opravy mnoha chyb.</span><span class="sxs-lookup"><span data-stu-id="c6e45-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="c6e45-190">Úplný seznam pracovní položky pevná ve NuGet 2.0, prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="c6e45-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
