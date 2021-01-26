---
title: Zpráva k vydání verze NuGet 2,1
description: Poznámky k verzi pro NuGet 2,1, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777032"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="6e001-103">Zpráva k vydání verze NuGet 2,1</span><span class="sxs-lookup"><span data-stu-id="6e001-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="6e001-104">Zpráva k [vydání verze](../release-notes/nuget-2.0.md)  |  NuGet 2,0 Zpráva k [vydání verze NuGet 2,2](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="6e001-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="6e001-105">NuGet 2,1 byl vydán 4. října 2012.</span><span class="sxs-lookup"><span data-stu-id="6e001-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="6e001-106">Hierarchické Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="6e001-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="6e001-107">NuGet 2,1 poskytuje větší flexibilitu při řízení nastavení NuGet pomocí způsobu rekurzivního procházení struktury složek, která hledá `NuGet.Config` soubory a pak sestaví konfiguraci ze sady všech nalezených souborů.</span><span class="sxs-lookup"><span data-stu-id="6e001-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="6e001-108">Můžete například zvážit scénář, ve kterém má tým interní úložiště balíčků pro sestavení CI jiných interních závislostí.</span><span class="sxs-lookup"><span data-stu-id="6e001-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="6e001-109">Struktura složky pro jednotlivý projekt může vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="6e001-109">The folder structure for an individual project might look like the following:</span></span>

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

<span data-ttu-id="6e001-110">Kromě toho, pokud je pro řešení povoleno obnovení balíčku, bude také k dispozici následující složka:</span><span class="sxs-lookup"><span data-stu-id="6e001-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

```
C:\myteam\solution1\.nuget
```

<span data-ttu-id="6e001-111">Aby bylo k dispozici interní úložiště balíčků týmu pro všechny projekty, na kterých tým pracuje, a ne tak, aby byl k dispozici pro každý projekt v počítači, můžeme vytvořit nový soubor Nuget.Config a umístit ho do složky c:\myteam.</span><span class="sxs-lookup"><span data-stu-id="6e001-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="6e001-112">Neexistuje žádný způsob, jak určit složku balíčků pro každý projekt.</span><span class="sxs-lookup"><span data-stu-id="6e001-112">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="6e001-113">Teď vidíte, že byl zdroj přidaný, spuštěním příkazu nuget.exe sources z jakékoli složky pod c:\myteam, jak je znázorněno níže:</span><span class="sxs-lookup"><span data-stu-id="6e001-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Zdroje balíčků z nadřazené konfigurace NuGet](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="6e001-115">`NuGet.Config` soubory jsou vyhledány v následujícím pořadí:</span><span class="sxs-lookup"><span data-stu-id="6e001-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="6e001-116">Rekurzivní procházení ze složky projektu do kořenového adresáře</span><span class="sxs-lookup"><span data-stu-id="6e001-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="6e001-117">Globální `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )</span><span class="sxs-lookup"><span data-stu-id="6e001-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="6e001-118">Konfigurace jsou nepoužitelné v *obráceném pořadí*, což znamená, že na základě výše uvedeného řazení by se nejdřív použily globální Nuget.Config a za ním byly zjištěné Nuget.Config soubory z kořenové složky do složky projektu `.nuget\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="6e001-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="6e001-119">To je obzvláště důležité, pokud používáte `<clear/>` element k odebrání sady položek z konfigurace.</span><span class="sxs-lookup"><span data-stu-id="6e001-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="6e001-120">Zadejte umístění složky Packages.</span><span class="sxs-lookup"><span data-stu-id="6e001-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="6e001-121">V minulosti měl NuGet spravované balíčky řešení ze známé složky Packages, která se nachází pod kořenovou složkou řešení.</span><span class="sxs-lookup"><span data-stu-id="6e001-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="6e001-122">Pro vývojové týmy, které mají nainstalovanou spoustu různých řešení s nainstalovanými balíčky NuGet, to může mít za následek instalaci stejného balíčku na mnoho různých míst v systému souborů.</span><span class="sxs-lookup"><span data-stu-id="6e001-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="6e001-123">NuGet 2,1 poskytuje podrobnější kontrolu nad umístěním složky Packages prostřednictvím `repositoryPath` elementu v `NuGet.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="6e001-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="6e001-124">Při sestavování v předchozím příkladu hierarchické podpory Nuget.Config Předpokládejme, že chceme, aby všechny projekty v rámci C:\myteam\ sdílely stejnou složku balíčků.</span><span class="sxs-lookup"><span data-stu-id="6e001-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="6e001-125">K tomu stačí přidat následující položku do `c:\myteam\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="6e001-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="6e001-126">V tomto příkladu sdílený `Nuget.Config` soubor Určuje složku sdílené balíčky pro každý projekt, který je vytvořen pod C:\myteam, bez ohledu na hloubku.</span><span class="sxs-lookup"><span data-stu-id="6e001-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="6e001-127">Všimněte si, že pokud máte složku s balíčky pod kořenem řešení, je nutné ji odstranit předtím, než NuGet umístí balíčky do nového umístění.</span><span class="sxs-lookup"><span data-stu-id="6e001-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="6e001-128">Podpora přenosných knihoven</span><span class="sxs-lookup"><span data-stu-id="6e001-128">Support for Portable Libraries</span></span>

<span data-ttu-id="6e001-129">[Přenosné knihovny](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) jsou funkce, která je nejprve představena s rozhraním .NET 4, která umožňuje sestavit sestavení, která mohou fungovat bez úprav na různých platformách společnosti Microsoft, od verzí The.NET Framework po Silverlight až po Windows Phone a dokonce i Xbox 360 (i když v tuto chvíli nástroj NuGet nepodporuje cíl přenosové knihovny Xbox).</span><span class="sxs-lookup"><span data-stu-id="6e001-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="6e001-130">Rozšířením [konvencí](../create-packages/supporting-multiple-target-frameworks.md) pro verze a profily architektury balíčků NuGet 2,1 teď podporuje přenosné knihovny tím, že vám umožní vytvářet balíčky, které mají složené architektury a cílové `lib` složky profilu.</span><span class="sxs-lookup"><span data-stu-id="6e001-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="6e001-131">Jako příklad zvažte následující dostupné cílové platformy knihovny přenosných tříd.</span><span class="sxs-lookup"><span data-stu-id="6e001-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Dialogové okno pro vytvoření přenosné knihovny](./media/releasenotes-21-plib.png)

<span data-ttu-id="6e001-133">Po vytvoření knihovny a spuštění příkazu se `nuget.exe pack MyPortableProject.csproj` může zobrazit nová struktura složky balíčku přenositelné knihovny. prozkoumáte obsah vygenerovaného balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="6e001-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Rozložení balíčku přenosné knihovny](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="6e001-135">Jak vidíte, konvence názvu složky přenositelné knihovny se řídí vzorem "přenosné-{Framework 1} + {Framework n}", kde identifikátory rozhraní následují po existujícím [názvu rozhraní a konvenci verzí](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="6e001-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="6e001-136">Jedna výjimka pro název a konvence verze se nachází v identifikátoru rozhraní, který se používá pro Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="6e001-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="6e001-137">Tento moniker by měl používat název rozhraní WP (wp7, wp71 nebo WP8).</span><span class="sxs-lookup"><span data-stu-id="6e001-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="6e001-138">Pokud například použijete ' Silverlight-WP7 ', výsledkem bude chyba.</span><span class="sxs-lookup"><span data-stu-id="6e001-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="6e001-139">Při instalaci balíčku vytvořeného z této struktury složek teď může NuGet použít své rozhraní a pravidla profilů na více cílů, jak je uvedeno v názvu složky.</span><span class="sxs-lookup"><span data-stu-id="6e001-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="6e001-140">Pravidla pro porovnání se základními balíčky NuGet jsou principem, že "konkrétnější" cíle budou mít přednost před "méně specifickými".</span><span class="sxs-lookup"><span data-stu-id="6e001-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="6e001-141">To znamená, že monikery cílené na konkrétní platformu budou vždy upřednostňovány přes přenosné, pokud jsou obě kompatibilní s projektem.</span><span class="sxs-lookup"><span data-stu-id="6e001-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="6e001-142">Kromě toho, pokud je více přenosných cílů kompatibilní s projektem, NuGet bude preferovat, kde je sada podporovaných platforem "nejbližší", k projektu, který odkazuje na balíček.</span><span class="sxs-lookup"><span data-stu-id="6e001-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="6e001-143">Cílení na projekty Windows 8 a Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="6e001-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="6e001-144">Kromě přidání podpory pro cílení na přenositelné projekty knihovny poskytuje NuGet 2,1 nové monikery rozhraní pro projekty Windows 8 Store a Windows Phone 8 a také některé nové obecné monikery pro projekty Windows Store a Windows Phone, které budou snazší spravovat v budoucích verzích příslušných platforem.</span><span class="sxs-lookup"><span data-stu-id="6e001-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="6e001-145">Pro aplikace Windows 8 Store tyto identifikátory vypadají takto:</span><span class="sxs-lookup"><span data-stu-id="6e001-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="6e001-146">NuGet 2,0 a starší</span><span class="sxs-lookup"><span data-stu-id="6e001-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="6e001-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="6e001-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="6e001-148">winRT45,. NETCore45</span><span class="sxs-lookup"><span data-stu-id="6e001-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="6e001-149">Windows, Windows8, Win, Win8</span><span class="sxs-lookup"><span data-stu-id="6e001-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="6e001-150">Pro Windows Phone projekty identifikátory vypadají takto:</span><span class="sxs-lookup"><span data-stu-id="6e001-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="6e001-151">Operační systém telefonu</span><span class="sxs-lookup"><span data-stu-id="6e001-151">Phone OS</span></span> | <span data-ttu-id="6e001-152">NuGet 2,0 a starší</span><span class="sxs-lookup"><span data-stu-id="6e001-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="6e001-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="6e001-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6e001-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="6e001-154">Windows Phone 7</span></span> | <span data-ttu-id="6e001-155">silverlight3 – WP</span><span class="sxs-lookup"><span data-stu-id="6e001-155">silverlight3-wp</span></span> | <span data-ttu-id="6e001-156">WP, wp7, WindowsPhone, WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="6e001-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="6e001-157">Windows Phone 7,5 (mango)</span><span class="sxs-lookup"><span data-stu-id="6e001-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="6e001-158">silverlight4-wp71</span><span class="sxs-lookup"><span data-stu-id="6e001-158">silverlight4-wp71</span></span> | <span data-ttu-id="6e001-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="6e001-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="6e001-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="6e001-160">Windows Phone 8</span></span> | <span data-ttu-id="6e001-161">(Nepodporováno)</span><span class="sxs-lookup"><span data-stu-id="6e001-161">(not supported)</span></span> | <span data-ttu-id="6e001-162">WP8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="6e001-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="6e001-163">Ve všech výše uvedených změnách budou staré názvy rozhraní nadále plně podporovány NuGet 2,1.</span><span class="sxs-lookup"><span data-stu-id="6e001-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="6e001-164">V rámci přesunu dopředu by se nové názvy měly používat, protože budou v budoucích verzích příslušných platforem stabilnější.</span><span class="sxs-lookup"><span data-stu-id="6e001-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="6e001-165">Nové názvy se ve verzích NuGet starších než 2,1 *nepodporují,* takže si je ale podle potřeby zajistěte, aby se tento přepínač naplánoval.</span><span class="sxs-lookup"><span data-stu-id="6e001-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="6e001-166">Vylepšené vyhledávání v dialogovém okně Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="6e001-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="6e001-167">V průběhu několika předchozích iterací byly do galerie NuGet zavedeny změny, které výrazně zlepšily rychlost a závažnost prohledávání balíčku.</span><span class="sxs-lookup"><span data-stu-id="6e001-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="6e001-168">Tato vylepšení se ale omezila na web nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6e001-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="6e001-169">NuGet 2,1 nabízí vylepšené možnosti vyhledávání v dialogovém okně Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="6e001-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="6e001-170">Představte si například, že jste chtěli najít balíček služby Windows Azure Caching Preview.</span><span class="sxs-lookup"><span data-stu-id="6e001-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="6e001-171">Přiměřený vyhledávací dotaz pro tento balíček může být "Azure cache".</span><span class="sxs-lookup"><span data-stu-id="6e001-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="6e001-172">V předchozích verzích dialogu Správce balíčků se požadovaný balíček ani na první stránce výsledků neuvádí.</span><span class="sxs-lookup"><span data-stu-id="6e001-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="6e001-173">V NuGet 2,1 se ale požadovaný balíček teď zobrazuje v horní části výsledků hledání.</span><span class="sxs-lookup"><span data-stu-id="6e001-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Hledání v dialogovém okně Správce balíčků](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="6e001-175">Vynutit aktualizaci balíčku</span><span class="sxs-lookup"><span data-stu-id="6e001-175">Force Package Update</span></span>

<span data-ttu-id="6e001-176">Před NuGet 2,1 by NuGet přeskočil aktualizaci balíčku, pokud se nejedná o číslo vysoké verze.</span><span class="sxs-lookup"><span data-stu-id="6e001-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="6e001-177">Tím bylo zavedeno tření pro určité scénáře – zejména v případě scénářů sestavení nebo CI, kdy tým nechtěl zvýšit číslo verze balíčku u každého sestavení.</span><span class="sxs-lookup"><span data-stu-id="6e001-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="6e001-178">Požadované chování bylo vynucovat bez ohledu na aktualizaci.</span><span class="sxs-lookup"><span data-stu-id="6e001-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="6e001-179">NuGet 2,1 tuto adresu řeší příznakem "přeinstalace".</span><span class="sxs-lookup"><span data-stu-id="6e001-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="6e001-180">Například při pokusu o aktualizaci balíčku, který nemá novější verzi balíčku, by měly být v předchozích verzích NuGet následující:</span><span class="sxs-lookup"><span data-stu-id="6e001-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

<span data-ttu-id="6e001-181">Pomocí příznaku přeinstalace se balíček aktualizuje bez ohledu na to, jestli existuje novější verze.</span><span class="sxs-lookup"><span data-stu-id="6e001-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

<span data-ttu-id="6e001-182">Dalším scénářem, kdy příznak opětovného navýšení projevuje, je to, že rozhraní cílí na cílení.</span><span class="sxs-lookup"><span data-stu-id="6e001-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="6e001-183">Při změně cílové architektury projektu (například z rozhraní .NET 4 na rozhraní .NET 4,5) může Update-Package-REINSTALL aktualizovat odkazy na správná sestavení pro všechny balíčky NuGet nainstalované v projektu.</span><span class="sxs-lookup"><span data-stu-id="6e001-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="6e001-184">Upravit zdroje balíčků v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6e001-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="6e001-185">V předchozích verzích NuGet aktualizoval zdroj balíčku z dialogového okna Možnosti sady Visual Studio, které vyžaduje odstranění a opětovné přidání zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="6e001-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="6e001-186">NuGet 2,1 vylepšuje tento pracovní postup díky podpoře aktualizace jako funkce první třídy uživatelského rozhraní konfigurace.</span><span class="sxs-lookup"><span data-stu-id="6e001-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Dialogové okno Konfigurace Správce balíčků](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="6e001-188">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="6e001-188">Bug Fixes</span></span>

<span data-ttu-id="6e001-189">NuGet 2,1 obsahuje mnoho oprav chyb.</span><span class="sxs-lookup"><span data-stu-id="6e001-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="6e001-190">Úplný seznam pracovních položek opravených v NuGet 2,0 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="6e001-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
