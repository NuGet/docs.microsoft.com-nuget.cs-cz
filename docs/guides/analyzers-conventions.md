---
title: Formáty analyzátoru kompilátoru .NET pro NuGet
description: Konvence pro analyzátory .NET, které jsou zabaleny a distribuovány s balíčky NuGet, které implementují rozhraní API nebo knihovny.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 4d337299f725b38981b0121069d5e6295b05e34e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "72924629"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="ae652-103">Analyzátor NuGet formáty</span><span class="sxs-lookup"><span data-stu-id="ae652-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="ae652-104">Platforma kompilátoru .NET (označovaná také jako "Roslyn") umožňuje vývojářům vytvářet [analyzátory,](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) které zkoumají strom syntaxe a sémantiku kódu při jeho zápisu.</span><span class="sxs-lookup"><span data-stu-id="ae652-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="ae652-105">To poskytuje vývojářům způsob, jak vytvořit nástroje pro analýzu specifické pro doménu, jako jsou ty, které by pomohly řídit použití konkrétního rozhraní API nebo knihovny.</span><span class="sxs-lookup"><span data-stu-id="ae652-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="ae652-106">Více informací najdete na wiki [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub.</span><span class="sxs-lookup"><span data-stu-id="ae652-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="ae652-107">Viz také [článek, Použijte Roslyn napsat Live Analyzátor kódu pro vaše rozhraní API](https://msdn.microsoft.com/magazine/dn879356.aspx) v MSDN Magazine.</span><span class="sxs-lookup"><span data-stu-id="ae652-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="ae652-108">Analyzátory samy o sobě jsou obvykle zabaleny a distribuovány jako součást nuget balíčky, které implementují rozhraní API nebo knihovny v otázce.</span><span class="sxs-lookup"><span data-stu-id="ae652-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="ae652-109">Dobrý příklad naleznete v balíčku [System.Runtime.Analyzers,](https://www.nuget.org/packages/System.Runtime.Analyzers) který má následující obsah:</span><span class="sxs-lookup"><span data-stu-id="ae652-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="ae652-110">analyzátory\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="ae652-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="ae652-111">analyzátory\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="ae652-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="ae652-112">analyzátory\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="ae652-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="ae652-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="ae652-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="ae652-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="ae652-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="ae652-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="ae652-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="ae652-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="ae652-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="ae652-117">nástroje\install.ps1</span><span class="sxs-lookup"><span data-stu-id="ae652-117">tools\install.ps1</span></span>
- <span data-ttu-id="ae652-118">nástroje\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="ae652-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="ae652-119">Jak můžete vidět, umístíte knihovny DLL `analyzers` analyzátoru do složky v balíčku.</span><span class="sxs-lookup"><span data-stu-id="ae652-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="ae652-120">Rekvizity soubory, které jsou zahrnuty zakázat starší FxCop pravidla ve `build` prospěch implementace analyzátoru, jsou umístěny ve složce.</span><span class="sxs-lookup"><span data-stu-id="ae652-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="ae652-121">Instalace a odinstalace skriptů, `packages.config` které `tools`podporují projekty pomocí jsou umístěny v aplikaci .</span><span class="sxs-lookup"><span data-stu-id="ae652-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="ae652-122">Všimněte si také, že vzhledem k `platform` tomu, že tento balíček nemá žádné požadavky specifické pro platformu, složka je vynechána.</span><span class="sxs-lookup"><span data-stu-id="ae652-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="ae652-123">Formát cesty analyzátorů</span><span class="sxs-lookup"><span data-stu-id="ae652-123">Analyzers path format</span></span>

<span data-ttu-id="ae652-124">Použití `analyzers` složky je podobné jako u [cílových architektur](../create-packages/supporting-multiple-target-frameworks.md), s výjimkou specifikátorů v cestě popisují závislosti hostitele vývoje namísto sestavení.</span><span class="sxs-lookup"><span data-stu-id="ae652-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="ae652-125">Obecný formát je následující:</span><span class="sxs-lookup"><span data-stu-id="ae652-125">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- <span data-ttu-id="ae652-126">**framework_name** a **verze**: *volitelná* plocha rozhraní API rozhraní .NET Framework, kterou musí spustit obsažené knihovny DLL.</span><span class="sxs-lookup"><span data-stu-id="ae652-126">**framework_name** and **version**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="ae652-127">`dotnet`je v současné době jedinou platnou hodnotu, protože Roslyn je jediný hostitel, který může spustit analyzátory.</span><span class="sxs-lookup"><span data-stu-id="ae652-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="ae652-128">Pokud není zadán žádný cíl, předpokládá se, že knihovny DLL se použijí na *všechny* cíle.</span><span class="sxs-lookup"><span data-stu-id="ae652-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="ae652-129">**supported_language**: jazyk, pro který se vztahuje `cs` dll, `vb` jeden z (C#) a (Visual Basic) a `fs` (F#).</span><span class="sxs-lookup"><span data-stu-id="ae652-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="ae652-130">Jazyk označuje, že analyzátor by měl být načten pouze pro projekt používající tento jazyk.</span><span class="sxs-lookup"><span data-stu-id="ae652-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="ae652-131">Pokud není zadán žádný jazyk, předpokládá se, že dll se vztahuje na *všechny* jazyky, které podporují analyzátory.</span><span class="sxs-lookup"><span data-stu-id="ae652-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="ae652-132">**analyzer_name**: určuje knihovny DLL analyzátoru.</span><span class="sxs-lookup"><span data-stu-id="ae652-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="ae652-133">Pokud potřebujete další soubory nad rámec knihoven DLL, musí být zahrnuty prostřednictvím souborů cílů nebo vlastností.</span><span class="sxs-lookup"><span data-stu-id="ae652-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="ae652-134">Instalace a odinstalace skriptů</span><span class="sxs-lookup"><span data-stu-id="ae652-134">Install and uninstall scripts</span></span>

<span data-ttu-id="ae652-135">Pokud projekt uživatele `packages.config`používá , skript MSBuild, který vyzvedne analyzátor nevstoupí do `install.ps1` hry, takže byste měli umístit a `uninstall.ps1` ve `tools` složce s obsahem, které jsou popsány níže.</span><span class="sxs-lookup"><span data-stu-id="ae652-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="ae652-136">**install.ps1 obsah souboru**</span><span class="sxs-lookup"><span data-stu-id="ae652-136">**install.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Install the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Install language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}
```


<span data-ttu-id="ae652-137">**odinstalovat soubor PS1**</span><span class="sxs-lookup"><span data-stu-id="ae652-137">**uninstall.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                try
                {
                    $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
                }
                catch
                {

                }
            }
        }
    }
}
```
