---
title: Poznámky k verzi 2.1 NuGet
description: Zpráva k vydání verze NuGet 2.1, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548594"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="82f85-103">Poznámky k verzi 2.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="82f85-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="82f85-104">[Zpráva k vydání verze NuGet 2.0](../release-notes/nuget-2.0.md) | [zpráva k vydání verze NuGet 2.2](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="82f85-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="82f85-105">NuGet 2.1 byla vydána 4. října 2012.</span><span class="sxs-lookup"><span data-stu-id="82f85-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="82f85-106">Hierarchické soubor Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="82f85-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="82f85-107">NuGet 2.1 získáte větší flexibilitu při řízení nastavení NuGet prostřednictvím rekurzivně walking nahoru strukturu složek hledání `NuGet.Config` soubory a pak sestavení konfigurace ze sady všechny nalezené soubory.</span><span class="sxs-lookup"><span data-stu-id="82f85-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="82f85-108">Jako příklad vezměte v úvahu scénář, ve kterém má tým jako interní balíček úložiště pro průběžné integrované sestavení další vnitřní závislosti.</span><span class="sxs-lookup"><span data-stu-id="82f85-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="82f85-109">Struktura složek pro jednotlivé projekt může vypadat nějak takto:</span><span class="sxs-lookup"><span data-stu-id="82f85-109">The folder structure for an individual project might look like the following:</span></span>

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

<span data-ttu-id="82f85-110">Kromě toho pokud obnovení balíčků je povolená pro řešení, do následující složky budou také existovat:</span><span class="sxs-lookup"><span data-stu-id="82f85-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

    C:\myteam\solution1\.nuget

<span data-ttu-id="82f85-111">Abyste měli úložiště interní balíček týmu k dispozici pro všechny projekty, které tým pracuje na, zároveň nejsou k dispozici pro každý projekt na počítači, můžeme vytvořte nový soubor Nuget.Config a umístěte ho do složky c:\myteam.</span><span class="sxs-lookup"><span data-stu-id="82f85-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="82f85-112">Neexistuje žádný způsob pro zadejte složku balíčků každý projekt.</span><span class="sxs-lookup"><span data-stu-id="82f85-112">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="82f85-113">Můžeme nyní vidět, že byl přidán zdroj spuštěním příkazu 'nuget.exe zdroje' z libovolné složky pod c:\myteam jak je znázorněno níže:</span><span class="sxs-lookup"><span data-stu-id="82f85-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Zdroje balíčků z konfigurace nadřazené nuget](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="82f85-115">`NuGet.Config` soubory se vyhledávají v následujícím pořadí:</span><span class="sxs-lookup"><span data-stu-id="82f85-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="82f85-116">Provede rekurzivní ze složky projektu do kořenového adresáře</span><span class="sxs-lookup"><span data-stu-id="82f85-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="82f85-117">Globální `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span><span class="sxs-lookup"><span data-stu-id="82f85-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="82f85-118">Tyto konfigurace se než v použít *pořadí*, to znamená, že podle výše uvedených řazení, globální Nuget.Config by být použije první, za nímž následuje zjištěných Nuget.Config soubory z kořenového adresáře do složky projektu, a potom podle `.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="82f85-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="82f85-119">To je zvlášť důležité, pokud používáte `<clear/>` prvek, který chcete odebrat z konfigurace sady položek.</span><span class="sxs-lookup"><span data-stu-id="82f85-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="82f85-120">Zadejte "balíčků' umístění složky</span><span class="sxs-lookup"><span data-stu-id="82f85-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="82f85-121">V minulosti má NuGet se spravovaným balíčků řešení ze složky známé "packages" nalezena pod kořenové složky řešení.</span><span class="sxs-lookup"><span data-stu-id="82f85-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="82f85-122">Pro vývojové týmy, které mají mnoho různých řešení, které mají nainstalované balíčky NuGet to může způsobit stejného balíčku instaluje v mnoha různých míst v systému souborů.</span><span class="sxs-lookup"><span data-stu-id="82f85-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="82f85-123">NuGet 2.1 poskytuje podrobnější kontrolu nad umístění složky balíčků prostřednictvím `repositoryPath` prvek `NuGet.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="82f85-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="82f85-124">Staví na předchozí příklad podporu hierarchických Nuget.Config, se předpokládá, že chceme mít všechny projekty v rámci C:\myteam\ sdílet stejnou složku balíčků.</span><span class="sxs-lookup"><span data-stu-id="82f85-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="82f85-125">K tomu jednoduše přidejte následující položku do `c:\myteam\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="82f85-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="82f85-126">V tomto příkladu, sdílený `Nuget.Config` souboru určuje sdílených balíčků složku pro každý projekt, který je vytvořen pod C:\myteam, bez ohledu na to hloubku.</span><span class="sxs-lookup"><span data-stu-id="82f85-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="82f85-127">Poznámka: Pokud máte existující složku balíčků pod kořenového adresáře řešení, musíte odstranit ho před NuGet umístí balíčky v novém umístění.</span><span class="sxs-lookup"><span data-stu-id="82f85-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="82f85-128">Podpora pro přenosné knihovny</span><span class="sxs-lookup"><span data-stu-id="82f85-128">Support for Portable Libraries</span></span>

<span data-ttu-id="82f85-129">[Přenosné knihovny](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) je funkce zavedená pomocí rozhraní .NET 4, která umožňuje vytvářet sestavení, které budou fungovat bez úprav na různých platformách společnosti Microsoft, od verzí rozhraní.NET Framework pro Silverlight pro Windows Phone a Xbox i 360 (i když se v tuto chvíli nepodporuje NuGet cílové Xbox přenosné knihovny).</span><span class="sxs-lookup"><span data-stu-id="82f85-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="82f85-130">Tím, že rozšíří [balíček konvence](../create-packages/supporting-multiple-target-frameworks.md) profilů a verze rozhraní framework NuGet 2.1 teď podporuje přenosných knihoven tím, že vám vytvořit balíčky, které mají složené framework a profil cílového `lib` složek.</span><span class="sxs-lookup"><span data-stu-id="82f85-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="82f85-131">Jako příklad zvažte následující knihovny přenosných tříd k dispozici cílové platformy.</span><span class="sxs-lookup"><span data-stu-id="82f85-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Dialogové okno Vytvoření přenosné knihovny](./media/releasenotes-21-plib.png)

<span data-ttu-id="82f85-133">Po sestavení knihovny a příkaz `nuget.exe pack MyPortableProject.csproj` spuštění nové přenosné knihovny struktury složky balíčku můžou vidět zkoumání obsahu vygenerovaný balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="82f85-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Přenosná knihovna rozložení balíčku](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="82f85-135">Jak je vidět, konvence název složky přenosné knihovny odpovídá vzoru "portable-{framework 1} + {framework n}" kde identifikátory framework použijte existující [konvence název a verzi rozhraní framework](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="82f85-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="82f85-136">Jedinou výjimkou konvence názvem a verzí se nachází v rámci identifikátor použitý pro Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="82f85-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="82f85-137">Tento zástupný název by měl použít název rozhraní "wp" (wp7, wp71 nebo wp8).</span><span class="sxs-lookup"><span data-stu-id="82f85-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="82f85-138">Použití "wp7 silverlight", například způsobí chybu.</span><span class="sxs-lookup"><span data-stu-id="82f85-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="82f85-139">Při instalaci balíčku, který je vytvořen z tuto strukturu složek, NuGet teď používat jeho rozhraní framework a profil pravidla více cílů, jak je uvedeno ve složce s názvem.</span><span class="sxs-lookup"><span data-stu-id="82f85-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="82f85-140">Za pravidla pro porovnávání NuGet je Princip "konkrétnější" cíle má přednost před těmi "specifické pro less".</span><span class="sxs-lookup"><span data-stu-id="82f85-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="82f85-141">To znamená, že monikery cílení na konkrétní platformu vždy upřednostňované nad přenosné ty Pokud jsou oba kompatibilní s projektem.</span><span class="sxs-lookup"><span data-stu-id="82f85-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="82f85-142">Kromě toho pokud více přenosné cíle jsou kompatibilní s projektem, NuGet preferovali jeden, kde je "nejbližší" do projektu balíček odkazování na sadu podporované platformy.</span><span class="sxs-lookup"><span data-stu-id="82f85-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="82f85-143">Cílení na Windows 8 a Windows Phone 8 projekty</span><span class="sxs-lookup"><span data-stu-id="82f85-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="82f85-144">Kromě přidání podpory pro cílení na projekty přenosných knihoven, NuGet 2.1 poskytuje nové rozhraní framework monikery pro projekty Windows Store 8 a Windows Phone 8, jakož i některé nové obecné monikery pro Windows Store a Windows Phone projekty, které budou snazší správa v budoucích verzích příslušné platformy.</span><span class="sxs-lookup"><span data-stu-id="82f85-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="82f85-145">Identifikátory pro aplikace Windows Store 8 vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="82f85-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="82f85-146">NuGet 2.0 a starší</span><span class="sxs-lookup"><span data-stu-id="82f85-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="82f85-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="82f85-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="82f85-148">winRT45, .NETCore45</span><span class="sxs-lookup"><span data-stu-id="82f85-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="82f85-149">Windows, Windows8, Windows, win8</span><span class="sxs-lookup"><span data-stu-id="82f85-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="82f85-150">Pro projekty Windows Phone identifikátory vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="82f85-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="82f85-151">Phone OS</span><span class="sxs-lookup"><span data-stu-id="82f85-151">Phone OS</span></span> | <span data-ttu-id="82f85-152">NuGet 2.0 a starší</span><span class="sxs-lookup"><span data-stu-id="82f85-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="82f85-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="82f85-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="82f85-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="82f85-154">Windows Phone 7</span></span> | <span data-ttu-id="82f85-155">silverlight3-wp</span><span class="sxs-lookup"><span data-stu-id="82f85-155">silverlight3-wp</span></span> | <span data-ttu-id="82f85-156">webové části, WindowsPhone7 wp7 WindowsPhone,</span><span class="sxs-lookup"><span data-stu-id="82f85-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="82f85-157">Windows Phone 7.5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="82f85-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="82f85-158">silverlight4 wp71</span><span class="sxs-lookup"><span data-stu-id="82f85-158">silverlight4-wp71</span></span> | <span data-ttu-id="82f85-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="82f85-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="82f85-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="82f85-160">Windows Phone 8</span></span> | <span data-ttu-id="82f85-161">(nepodporováno)</span><span class="sxs-lookup"><span data-stu-id="82f85-161">(not supported)</span></span> | <span data-ttu-id="82f85-162">wp8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="82f85-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="82f85-163">Ve všech výše uvedené změny bude nadále staré názvy framework plné podpory společností NuGet 2.1.</span><span class="sxs-lookup"><span data-stu-id="82f85-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="82f85-164">V budoucnu, nové názvy by měla sloužit jako, v budoucích verzích příslušné platformy bude stabilnější.</span><span class="sxs-lookup"><span data-stu-id="82f85-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="82f85-165">Nové názvy se *není* se nepodporuje v verze NuGet starší než 2.1, ale to podle toho naplánujte pro případ přechod usnadní.</span><span class="sxs-lookup"><span data-stu-id="82f85-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="82f85-166">Vylepšené vyhledávání v dialogovém okně Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="82f85-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="82f85-167">V posledních několika iterací změny byly zavedeny do Galerie NuGet, který výrazně zlepšit rychlost a relevance vyhledávání balíčků.</span><span class="sxs-lookup"><span data-stu-id="82f85-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="82f85-168">Nicméně tato vylepšení byla omezena na webu nuget.org.</span><span class="sxs-lookup"><span data-stu-id="82f85-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="82f85-169">NuGet 2.1 zpřístupňuje vylepšené vyhledávání prostředí přes dialogové okno Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="82f85-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="82f85-170">Jako příklad Představte si, že byste chtěli najít balíček ve verzi Preview ukládání do mezipaměti na Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="82f85-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="82f85-171">"Azure Cache" může být rozumné vyhledávací dotaz pro tento balíček.</span><span class="sxs-lookup"><span data-stu-id="82f85-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="82f85-172">V předchozích verzích dialogové okno Správce balíčků nebude požadovaný balíček i uvedena na první stránku výsledků.</span><span class="sxs-lookup"><span data-stu-id="82f85-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="82f85-173">Ale v NuGet 2.1 požadovaný balíček nyní zobrazí v horní části výsledků vyhledávání.</span><span class="sxs-lookup"><span data-stu-id="82f85-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Hledání dialogové okno Správce balíčků](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="82f85-175">Vynucení aktualizace balíčku</span><span class="sxs-lookup"><span data-stu-id="82f85-175">Force Package Update</span></span>

<span data-ttu-id="82f85-176">Před NuGet 2.1 NuGet by přeskočit aktualizace balíčku, pokud došlo a nikoli číslo vyšší číslo verze.</span><span class="sxs-lookup"><span data-stu-id="82f85-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="82f85-177">To zavedené případná problémová místa pro určité scénáře – zejména v případě sestavení nebo CI scénáře, ve kterém tým nechtěli zvyšovat číslo každé sestavení verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="82f85-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="82f85-178">Chcete vynutit aktualizaci bez ohledu na to je požadované chování.</span><span class="sxs-lookup"><span data-stu-id="82f85-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="82f85-179">NuGet 2.1 řeší to s příznakem "přeinstalovat".</span><span class="sxs-lookup"><span data-stu-id="82f85-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="82f85-180">Například předchozí verze balíčku nuget by výsledkem bylo toto při pokusu o aktualizaci balíčku, který nemá novější verze balíčku:</span><span class="sxs-lookup"><span data-stu-id="82f85-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

<span data-ttu-id="82f85-181">S příznakem reinstall bude aktualizován balíček bez ohledu na to, zda je k dispozici novější verze.</span><span class="sxs-lookup"><span data-stu-id="82f85-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

<span data-ttu-id="82f85-182">Jiný scénář, kde prokáže příznak reinstall výhodné je znovu cílení rozhraní.</span><span class="sxs-lookup"><span data-stu-id="82f85-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="82f85-183">Při změně cílové rozhraní projektu (například z .NET 4 na rozhraní .NET 4.5), Update-Package-přeinstalujte můžete aktualizovat odkazy na správné sestavení pro všechny balíčky NuGet v projektu nainstalován.</span><span class="sxs-lookup"><span data-stu-id="82f85-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="82f85-184">Upravit zdroje balíčků v rámci sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="82f85-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="82f85-185">V předchozích verzích balíčku nuget aktualizuje se zdroj balíčku z v rámci dialogové okno Možnosti sady Visual Studio vyžaduje odstranit a znovu přidat zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="82f85-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="82f85-186">NuGet 2.1 Tento pracovní postup zlepšuje podporu aktualizace jako funkce první třídy uživatelské rozhraní konfigurace.</span><span class="sxs-lookup"><span data-stu-id="82f85-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Dialogové okno Konfigurace Správce balíčků](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="82f85-188">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="82f85-188">Bug Fixes</span></span>

<span data-ttu-id="82f85-189">NuGet 2.1 obsahuje řadu oprav chyb.</span><span class="sxs-lookup"><span data-stu-id="82f85-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="82f85-190">Úplný seznam pracovních položek opravených NuGet 2.0 prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="82f85-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
