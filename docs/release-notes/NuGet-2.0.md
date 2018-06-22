---
title: Poznámky k verzi 2.0 NuGet
description: Poznámky k verzi pro NuGet 2.0 včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0e637a953d9d5d10394857a352be96a7f68dc4e8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820794"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="379ac-103">Poznámky k verzi 2.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="379ac-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="379ac-104">[Poznámky k verzi NuGet 1.8](../release-notes/nuget-1.8.md) | [NuGet 2.1 poznámky k verzi](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="379ac-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="379ac-105">NuGet 2.0 byla vydána 19. června 2012.</span><span class="sxs-lookup"><span data-stu-id="379ac-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="379ac-106">Instalace známý problém</span><span class="sxs-lookup"><span data-stu-id="379ac-106">Known Installation Issue</span></span>
<span data-ttu-id="379ac-107">Pokud používáte VS 2010 SP1, můžete spustit došlo k chybě instalace při pokusu o upgrade NuGet, pokud máte nainstalovaný starší verze.</span><span class="sxs-lookup"><span data-stu-id="379ac-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="379ac-108">Alternativní řešení je jednoduše odinstalovat NuGet a nainstalujte ji z Galerie rozšíření VS.</span><span class="sxs-lookup"><span data-stu-id="379ac-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="379ac-109">V tématu [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Další informace, nebo [přejděte přímo na opravu hotfix VS](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="379ac-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="379ac-110">Poznámka: Pokud Visual Studio nebude možné odinstalovat rozšíření (k dispozici tlačítko Odinstalovat), bude pravděpodobně nutné restartujte Visual Studio pomocí "Spustit jako správce."</span><span class="sxs-lookup"><span data-stu-id="379ac-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="379ac-111">Balíček souhlasu obnovení je teď aktivní</span><span class="sxs-lookup"><span data-stu-id="379ac-111">Package restore consent is now active</span></span>

<span data-ttu-id="379ac-112">Jak je popsáno v tomto [můžete zveřejnit na balíček obnovení souhlasu](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 nyní vyžadují souhlasu umožňující obnovení balíčků přejděte do režimu online a stáhnout balíčky.</span><span class="sxs-lookup"><span data-stu-id="379ac-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="379ac-113">Zkontrolujte, zda jste zadali souhlasu prostřednictvím dialogu konfigurace správce balíčku nebo proměnné prostředí EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="379ac-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="379ac-114">Závislosti skupiny podle cílové rozhraní</span><span class="sxs-lookup"><span data-stu-id="379ac-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="379ac-115">Od verze 2.0, balíčku, který se může lišit v závislosti na základě framework profilu cíl projektu.</span><span class="sxs-lookup"><span data-stu-id="379ac-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="379ac-116">Toho dosahuje pomocí aktualizované `.nuspec` schématu.</span><span class="sxs-lookup"><span data-stu-id="379ac-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="379ac-117">`<dependencies>` Element může obsahovat teď sadu `<group>` elementy.</span><span class="sxs-lookup"><span data-stu-id="379ac-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="379ac-118">Každá skupina obsahuje nula nebo více `<dependency>` elementy a `targetFramework` atribut.</span><span class="sxs-lookup"><span data-stu-id="379ac-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="379ac-119">Pokud cílovém Frameworku, který je kompatibilní s profilem cílový framework projektu byly společně nainstalované všechny závislosti uvnitř skupiny.</span><span class="sxs-lookup"><span data-stu-id="379ac-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="379ac-120">Příklad:</span><span class="sxs-lookup"><span data-stu-id="379ac-120">For example:</span></span>

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

<span data-ttu-id="379ac-121">Všimněte si, že skupina může obsahovat **nula** závislosti.</span><span class="sxs-lookup"><span data-stu-id="379ac-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="379ac-122">V příkladu nahoře Pokud tento balíček je nainstalovaný do projektu, jehož cílem Silverlight 3.0 nebo novější, nemá žádné závislosti budou nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="379ac-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="379ac-123">Pokud balíček je nainstalovaný do projektu, jehož cílem rozhraní .NET 4.0 nebo novější, obě závislosti, jQuery a WebActivator, budou nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="379ac-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="379ac-124">Pokud instalaci balíčku do projektu, jehož cílem starší verzí tyto 2 architektury nebo jiných framework RouteMagic 1.1.0 se nainstaluje.</span><span class="sxs-lookup"><span data-stu-id="379ac-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="379ac-125">Neexistuje žádné dědičnosti mezi skupinami.</span><span class="sxs-lookup"><span data-stu-id="379ac-125">There is no inheritance between groups.</span></span> <span data-ttu-id="379ac-126">Pokud cílový framework projektu na odpovídá `targetFramework` nainstaluje atribut skupiny jenom závislosti v rámci dané skupiny.</span><span class="sxs-lookup"><span data-stu-id="379ac-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="379ac-127">Balíček můžete určit závislosti balíčků v některém z dva formáty: starý formát plochý seznam `<dependency>` elementy nebo skupiny.</span><span class="sxs-lookup"><span data-stu-id="379ac-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="379ac-128">Pokud `<group>` použít formát, balíček nelze nainstalovat do verze NuGet starší než 2.0.</span><span class="sxs-lookup"><span data-stu-id="379ac-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="379ac-129">Všimněte si, že kombinování dvěma formáty není povolené.</span><span class="sxs-lookup"><span data-stu-id="379ac-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="379ac-130">Například následující fragment kódu je **neplatný** a budou odmítnuty systémem NuGet.</span><span class="sxs-lookup"><span data-stu-id="379ac-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="379ac-131">Seskupování podle cílové rozhraní soubory obsahu a skriptů prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="379ac-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="379ac-132">Kromě odkazy na sestavení soubory obsahu a skriptů prostředí PowerShell můžete taky Seskupit podle cílové rozhraní.</span><span class="sxs-lookup"><span data-stu-id="379ac-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="379ac-133">Stejnou strukturu složek najít v `lib` složku pro zadání cílové rozhraní je nyní možné použít v stejným způsobem, jako `content` a `tools` složek.</span><span class="sxs-lookup"><span data-stu-id="379ac-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="379ac-134">Příklad:</span><span class="sxs-lookup"><span data-stu-id="379ac-134">For example:</span></span>

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

<span data-ttu-id="379ac-135">**Poznámka:**: protože `init.ps1` je proveden na úrovni řešení a není závislá na všech jednotlivých projektů, je nutné ji umístit přímo pod `tools` složky.</span><span class="sxs-lookup"><span data-stu-id="379ac-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="379ac-136">Pokud se umístit do složky pro konkrétní rozhraní, se budou ignorovat.</span><span class="sxs-lookup"><span data-stu-id="379ac-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="379ac-137">Novou funkcí systému NuGet 2.0 je také, že lze složku rozhraní *prázdný*, v takovém případě nebude přidejte odkazy na sestavení, přidání souborů obsahu nebo spuštění skriptů prostředí PowerShell pro konkrétní verzi NuGet.</span><span class="sxs-lookup"><span data-stu-id="379ac-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="379ac-138">V příkladu výše, složce `content\net40` je prázdný.</span><span class="sxs-lookup"><span data-stu-id="379ac-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="379ac-139">Vylepšené karta dokončení výkonu</span><span class="sxs-lookup"><span data-stu-id="379ac-139">Improved tab completion performance</span></span>
<span data-ttu-id="379ac-140">Funkci karta dokončení v konzole Správce balíčků NuGet se aktualizovalo a výrazně zlepšit výkon.</span><span class="sxs-lookup"><span data-stu-id="379ac-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="379ac-141">Bude mnohem menší zpoždění od okamžiku, kdy stisknutí klávesy tab, až se zobrazí rozevírací seznam návrhu.</span><span class="sxs-lookup"><span data-stu-id="379ac-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="379ac-142">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="379ac-142">Bug Fixes</span></span>
<span data-ttu-id="379ac-143">NuGet 2.0 zahrnuje mnoho opravy chyb s důrazem na balíček obnovení souhlasu a výkonu.</span><span class="sxs-lookup"><span data-stu-id="379ac-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="379ac-144">Úplný seznam pracovní položky pevná ve NuGet 2.0, prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="379ac-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
