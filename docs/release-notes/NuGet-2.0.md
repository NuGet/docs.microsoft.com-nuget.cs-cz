---
title: Poznámky k verzi 2.0 NuGet
description: Zpráva k vydání verze NuGet 2.0, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547572"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="037c8-103">Poznámky k verzi 2.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="037c8-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="037c8-104">[Zpráva k vydání verze NuGet 1.8](../release-notes/nuget-1.8.md) | [zpráva k vydání verze NuGet 2.1](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="037c8-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="037c8-105">NuGet 2.0 vydané 19. června 2012.</span><span class="sxs-lookup"><span data-stu-id="037c8-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="037c8-106">Instalace známý problém</span><span class="sxs-lookup"><span data-stu-id="037c8-106">Known Installation Issue</span></span>
<span data-ttu-id="037c8-107">Pokud spustíte VS 2010 SP1, můžete narazit na chybu instalace při pokusu o upgradu Nugetu, pokud máte nainstalovaný starší verze.</span><span class="sxs-lookup"><span data-stu-id="037c8-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="037c8-108">Alternativním řešením je jednoduše odinstalovat NuGet a nainstalujte ho z Galerie rozšíření VS.</span><span class="sxs-lookup"><span data-stu-id="037c8-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="037c8-109">Zobrazit [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Další informace nebo [přejděte přímo na opravu hotfix VS](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="037c8-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="037c8-110">Poznámka: Pokud Visual Studio neumožní odinstalovat rozšíření (tlačítko Odinstalovat je vypnutá), pak pravděpodobně nutné restartovat Visual Studio pomocí příkazu "Spustit jako správce."</span><span class="sxs-lookup"><span data-stu-id="037c8-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="037c8-111">Souhlas obnovení balíčku je teď aktivní</span><span class="sxs-lookup"><span data-stu-id="037c8-111">Package restore consent is now active</span></span>

<span data-ttu-id="037c8-112">Jak je popsáno v tomto [Zveřejněte na souhlas obnovení balíčku](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 bude nyní vyžadovat souhlasu povolit obnovení balíčků přejít online a stáhnout balíčky.</span><span class="sxs-lookup"><span data-stu-id="037c8-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="037c8-113">Ujistěte se prosím, že jste zadali souhlasu prostřednictvím dialogu konfigurace Správce balíčků nebo proměnné prostředí EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="037c8-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="037c8-114">Skupina závislostí podle cílových platforem</span><span class="sxs-lookup"><span data-stu-id="037c8-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="037c8-115">Od verze 2.0, balíček, který se může lišit v závislosti na základě v rámci profilu na cílový projekt.</span><span class="sxs-lookup"><span data-stu-id="037c8-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="037c8-116">To lze provést pomocí aktualizovaného `.nuspec` schématu.</span><span class="sxs-lookup"><span data-stu-id="037c8-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="037c8-117">`<dependencies>` Element teď může obsahovat sadu `<group>` elementy.</span><span class="sxs-lookup"><span data-stu-id="037c8-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="037c8-118">Každá skupina obsahuje nula nebo více `<dependency>` elementy a `targetFramework` atribut.</span><span class="sxs-lookup"><span data-stu-id="037c8-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="037c8-119">Pokud cílová architektura, která je kompatibilní s profil cílového rozhraní framework projektu, jsou všechny závislosti uvnitř skupiny nainstalovaných společně.</span><span class="sxs-lookup"><span data-stu-id="037c8-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="037c8-120">Příklad:</span><span class="sxs-lookup"><span data-stu-id="037c8-120">For example:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<span data-ttu-id="037c8-121">Všimněte si, že skupina může obsahovat **nula** závislosti.</span><span class="sxs-lookup"><span data-stu-id="037c8-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="037c8-122">V předchozím příkladu Pokud je balíček nainstalován do projektu, který cílí na technologii Silverlight 3.0 nebo novější, nemá žádné závislosti se nainstaluje.</span><span class="sxs-lookup"><span data-stu-id="037c8-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="037c8-123">Pokud balíček je nainstalovaný do projektu, který cílí na rozhraní .NET 4.0 nebo novější, dvě závislosti, jQuery a WebActivator, se nainstalují.</span><span class="sxs-lookup"><span data-stu-id="037c8-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="037c8-124">Pokud je balíček nainstalován do projektu, který cílí na starší verzi aplikace tyto 2 architektury nebo libovolné jiné architektury, nainstaluje se RouteMagic 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="037c8-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="037c8-125">Neexistuje žádné dědičnosti mezi skupinami.</span><span class="sxs-lookup"><span data-stu-id="037c8-125">There is no inheritance between groups.</span></span> <span data-ttu-id="037c8-126">Pokud cílové rozhraní projektu odpovídá `targetFramework` atribut skupiny, jenom závislosti v rámci této skupiny se nainstaluje.</span><span class="sxs-lookup"><span data-stu-id="037c8-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="037c8-127">Balíček můžete určit závislosti balíčků v některém z dva formáty: starý formát plochý seznam `<dependency>` elementy nebo skupiny.</span><span class="sxs-lookup"><span data-stu-id="037c8-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="037c8-128">Pokud `<group>` formát se používá, balíček nejde nainstalovat do verze NuGet starší než 2.0.</span><span class="sxs-lookup"><span data-stu-id="037c8-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="037c8-129">Všimněte si, že míchání dva formáty nejsou povolené.</span><span class="sxs-lookup"><span data-stu-id="037c8-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="037c8-130">Například následující fragment kódu je **neplatný** a odmítne NuGet.</span><span class="sxs-lookup"><span data-stu-id="037c8-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="037c8-131">Seskupení obsahu soubory a skripty prostředí PowerShell pomocí rozhraní .NET framework</span><span class="sxs-lookup"><span data-stu-id="037c8-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="037c8-132">Kromě odkazů na sestavení soubory obsahu a skripty prostředí PowerShell můžete taky Seskupit podle cílovou architekturu.</span><span class="sxs-lookup"><span data-stu-id="037c8-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="037c8-133">Součástí stejné struktury složek `lib` složku pro zadání cílové rozhraní se teď může používat stejně jako na `content` a `tools` složek.</span><span class="sxs-lookup"><span data-stu-id="037c8-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="037c8-134">Příklad:</span><span class="sxs-lookup"><span data-stu-id="037c8-134">For example:</span></span>

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

<span data-ttu-id="037c8-135">**Poznámka:**: protože `init.ps1` provádí na úrovni řešení a není závislá na každý individuální projekt, se musí umístit přímo pod `tools` složky.</span><span class="sxs-lookup"><span data-stu-id="037c8-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="037c8-136">Pokud umístěné ve složce pro konkrétní rozhraní, bude se ignorovat.</span><span class="sxs-lookup"><span data-stu-id="037c8-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="037c8-137">Nová funkce ve verzi NuGet 2.0 je také, že framework složka může představovat *prázdný*, v takovém případě nebude přidat odkazy na sestavení, přidání souborů obsahu nebo spouštění skriptů prostředí PowerShell pro konkrétní framework verze NuGet.</span><span class="sxs-lookup"><span data-stu-id="037c8-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="037c8-138">V příkladu výše, složce `content\net40` je prázdný.</span><span class="sxs-lookup"><span data-stu-id="037c8-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="037c8-139">Vylepšené kartu dokončení výkonu</span><span class="sxs-lookup"><span data-stu-id="037c8-139">Improved tab completion performance</span></span>
<span data-ttu-id="037c8-140">Aktualizovali jsme funkci doplňování kartu v konzole Správce balíčků NuGet k výraznému zlepšení výkonu.</span><span class="sxs-lookup"><span data-stu-id="037c8-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="037c8-141">Bude mnohem menším zpoždění od okamžiku, kdy stisknutí klávesy tab, dokud se zobrazí rozevírací seznam návrhů.</span><span class="sxs-lookup"><span data-stu-id="037c8-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="037c8-142">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="037c8-142">Bug Fixes</span></span>
<span data-ttu-id="037c8-143">NuGet 2.0 obsahuje řadu oprav chyb s důrazem na souhlas obnovení balíčků a výkon.</span><span class="sxs-lookup"><span data-stu-id="037c8-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="037c8-144">Úplný seznam pracovních položek opravených NuGet 2.0 prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="037c8-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
