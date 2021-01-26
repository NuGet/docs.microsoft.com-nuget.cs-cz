---
title: Zpráva k vydání verze NuGet 2,0
description: Poznámky k verzi pro NuGet 2,0, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6874cbf0404f18ab7007bec1e0f66089c790d08
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776992"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="b902b-103">Zpráva k vydání verze NuGet 2,0</span><span class="sxs-lookup"><span data-stu-id="b902b-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="b902b-104">Zpráva k [vydání verze](../release-notes/nuget-1.8.md)  |  NuGet 1,8 Zpráva k [vydání verze NuGet 2,1](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="b902b-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="b902b-105">NuGet 2,0 byl vydán 19. června 2012.</span><span class="sxs-lookup"><span data-stu-id="b902b-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="b902b-106">Známý problém s instalací</span><span class="sxs-lookup"><span data-stu-id="b902b-106">Known Installation Issue</span></span>
<span data-ttu-id="b902b-107">Pokud používáte VS 2010 SP1, můžete při pokusu o upgrade NuGetu v případě, že máte nainstalovanou starší verzi, spustit chybu instalace.</span><span class="sxs-lookup"><span data-stu-id="b902b-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="b902b-108">Alternativním řešením je jednoduše odinstalovat NuGet a pak ji nainstalovat z galerie rozšíření VS.</span><span class="sxs-lookup"><span data-stu-id="b902b-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="b902b-109">Další informace najdete v tématu <https://support.microsoft.com/kb/2581019> , kde najdete další informace, nebo [přejděte přímo na opravu hotfix vs](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="b902b-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="b902b-110">Poznámka: Pokud Visual Studio neumožní odinstalovat rozšíření (tlačítko Odinstalace je zakázané), pak budete pravděpodobně muset restartovat Visual Studio pomocí možnosti Spustit jako správce.</span><span class="sxs-lookup"><span data-stu-id="b902b-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="b902b-111">Souhlasu balíčku pro obnovení je teď aktivní.</span><span class="sxs-lookup"><span data-stu-id="b902b-111">Package restore consent is now active</span></span>

<span data-ttu-id="b902b-112">Jak je popsáno v tomto [příspěvku o souhlasu s obnovením balíčku](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2,0 nyní vyžaduje souhlas s povolením, aby obnovení balíčků mohlo přejít online a stáhnout balíčky.</span><span class="sxs-lookup"><span data-stu-id="b902b-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="b902b-113">Ujistěte se prosím, že jste poskytli souhlas prostřednictvím dialogu konfigurace správce balíčků nebo proměnné prostředí EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="b902b-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="b902b-114">Seskupení závislostí podle cílových rozhraní</span><span class="sxs-lookup"><span data-stu-id="b902b-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="b902b-115">Počínaje verzí 2,0 se závislosti balíčků můžou lišit v závislosti na profilu rozhraní cílového projektu.</span><span class="sxs-lookup"><span data-stu-id="b902b-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="b902b-116">To je provedeno pomocí aktualizovaného `.nuspec` schématu.</span><span class="sxs-lookup"><span data-stu-id="b902b-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="b902b-117">`<dependencies>`Element může nyní obsahovat sadu `<group>` prvků.</span><span class="sxs-lookup"><span data-stu-id="b902b-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="b902b-118">Každá skupina obsahuje nula nebo více `<dependency>` elementů a `targetFramework` atribut.</span><span class="sxs-lookup"><span data-stu-id="b902b-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="b902b-119">Všechny závislosti v rámci skupiny jsou nainstalovány společně, pokud je cílový rámec kompatibilní s profilem cílového projektového architektury.</span><span class="sxs-lookup"><span data-stu-id="b902b-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="b902b-120">Například:</span><span class="sxs-lookup"><span data-stu-id="b902b-120">For example:</span></span>

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

<span data-ttu-id="b902b-121">Všimněte si, že skupina může obsahovat **nulové** závislosti.</span><span class="sxs-lookup"><span data-stu-id="b902b-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="b902b-122">Pokud se v předchozím příkladu nainstaluje balíček do projektu, který cílí na Silverlight 3,0 nebo novější, nebudou nainstalovány žádné závislosti.</span><span class="sxs-lookup"><span data-stu-id="b902b-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="b902b-123">Pokud je balíček nainstalován do projektu cíleného na rozhraní .NET 4,0 nebo novější, budou nainstalovány dvě závislosti, jQuery a webactivator.</span><span class="sxs-lookup"><span data-stu-id="b902b-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="b902b-124">Pokud se balíček nainstaluje do projektu, který se zaměřuje na počáteční verzi těchto 2 platforem, nebo na jakékoli jiné rozhraní, nainstaluje se RouteMagic 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="b902b-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="b902b-125">Mezi skupinami neexistuje žádná dědičnost.</span><span class="sxs-lookup"><span data-stu-id="b902b-125">There is no inheritance between groups.</span></span> <span data-ttu-id="b902b-126">Pokud cílové rozhraní projektu odpovídá `targetFramework` atributu skupiny, budou nainstalovány pouze závislosti v této skupině.</span><span class="sxs-lookup"><span data-stu-id="b902b-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="b902b-127">Balíček může určovat závislosti balíčků v jednom ze dvou formátů: ve starém formátu nestrukturovaného seznamu `<dependency>` prvků nebo skupin.</span><span class="sxs-lookup"><span data-stu-id="b902b-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="b902b-128">Při `<group>` použití formátu se balíček nedá nainstalovat do verzí NuGet starších než 2,0.</span><span class="sxs-lookup"><span data-stu-id="b902b-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="b902b-129">Všimněte si, že kombinace těchto dvou formátů není povolená.</span><span class="sxs-lookup"><span data-stu-id="b902b-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="b902b-130">Například následující fragment kódu je **neplatný** a bude NuGet odmítnut.</span><span class="sxs-lookup"><span data-stu-id="b902b-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="b902b-131">Seskupení souborů obsahu a skriptů PowerShellu podle cílové architektury</span><span class="sxs-lookup"><span data-stu-id="b902b-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="b902b-132">Kromě odkazů na sestavení je také možné seskupit soubory obsahu a skripty prostředí PowerShell podle cílové architektury.</span><span class="sxs-lookup"><span data-stu-id="b902b-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="b902b-133">Stejná struktura složek, která se nachází ve `lib` složce pro určení cílové architektury, se teď dá použít stejným způsobem jako `content` složky a `tools` .</span><span class="sxs-lookup"><span data-stu-id="b902b-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="b902b-134">Například:</span><span class="sxs-lookup"><span data-stu-id="b902b-134">For example:</span></span>

```
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
```

<span data-ttu-id="b902b-135">**Poznámka**: vzhledem k tomu `init.ps1` , že je provedena na úrovni řešení a není závislý na žádném jednotlivém projektu, musí být přímo pod `tools` složkou.</span><span class="sxs-lookup"><span data-stu-id="b902b-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="b902b-136">Pokud je umístěn do složky specifické pro rozhraní, bude ignorováno.</span><span class="sxs-lookup"><span data-stu-id="b902b-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="b902b-137">Nová funkce v NuGet 2,0 je taky to, že složka rozhraní může být *prázdná*. v takovém případě NuGet nepřidá odkazy na sestavení, přidá soubory obsahu nebo spustí skripty PowerShellu pro konkrétní verzi Frameworku.</span><span class="sxs-lookup"><span data-stu-id="b902b-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="b902b-138">Ve výše uvedeném příkladu `content\net40` je složka prázdná.</span><span class="sxs-lookup"><span data-stu-id="b902b-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="b902b-139">Vylepšený výkon dokončování karet</span><span class="sxs-lookup"><span data-stu-id="b902b-139">Improved tab completion performance</span></span>
<span data-ttu-id="b902b-140">Funkce dokončování karet v konzole správce balíčků NuGet se aktualizovala tak, aby významně zvýšila výkon.</span><span class="sxs-lookup"><span data-stu-id="b902b-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="b902b-141">Čas stisknutí klávesy TAB bude mnohem kratší, dokud se nezobrazí rozevírací seznam návrh.</span><span class="sxs-lookup"><span data-stu-id="b902b-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="b902b-142">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="b902b-142">Bug Fixes</span></span>
<span data-ttu-id="b902b-143">NuGet 2,0 obsahuje mnoho oprav chyb s důrazem na dodržování souhlasu a výkonu balíčku pro obnovení.</span><span class="sxs-lookup"><span data-stu-id="b902b-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="b902b-144">Úplný seznam pracovních položek opravených v NuGet 2,0 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="b902b-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
