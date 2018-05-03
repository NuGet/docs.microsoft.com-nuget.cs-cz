---
title: Rozhraní .NET kompilátoru platformy analyzátor formátech pro NuGet
description: Konvence pro analyzátory .NET, které se zabalí a distribuovat s balíčky NuGet, které implementují rozhraní API nebo knihovny.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 57ab485c8062b0515c292b68ecb5a3628b6e3e9d
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2018
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="c8a1d-103">Analyzátor NuGet formáty</span><span class="sxs-lookup"><span data-stu-id="c8a1d-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="c8a1d-104">Kompilátoru platformu .NET (také označované jako "Roslyn") umožňují vývojářům vytvářet [analyzátorů](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) , podívejte se na strom syntaxe a sémantiku kódu se zapsané.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-104">The .NET Compiler Platform (also known as "Roslyn") allow developers to create [analyzers](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="c8a1d-105">To poskytuje vývojářům způsob, jak vytvořit a specifické pro doménu analytické nástroje, jako jsou ty, které pomohou průvodce použít konkrétní rozhraní API nebo knihovny.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-105">This provides developers with a way to create and domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="c8a1d-106">Další informace najdete na [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) wiki Githubu.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="c8a1d-107">Také najdete v článku [Roslyn použití k zápisu Live analyzátor kódu pro vaše rozhraní API](https://msdn.microsoft.com/magazine/dn879356.aspx) v časopise MSDN.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="c8a1d-108">Analyzátory sami jsou obvykle zabalené a distribuovat jako součást balíčky NuGet, které implementují rozhraní API nebo knihovny nejistá.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="c8a1d-109">Dobrým příkladem, najdete v článku [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) balíček, který má následující obsah:</span><span class="sxs-lookup"><span data-stu-id="c8a1d-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="c8a1d-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="c8a1d-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="c8a1d-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="c8a1d-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="c8a1d-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="c8a1d-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="c8a1d-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="c8a1d-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="c8a1d-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="c8a1d-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="c8a1d-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="c8a1d-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="c8a1d-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="c8a1d-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="c8a1d-117">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="c8a1d-117">tools\install.ps1</span></span>
- <span data-ttu-id="c8a1d-118">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="c8a1d-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="c8a1d-119">Jak vidíte, umístíte analyzátor knihoven DLL do `analyzers` složky v balíčku.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="c8a1d-120">Soubory props, které jsou součástí zakázat zastaralá pravidla FxCop považuje implementace analyzátor, jsou umístěny v `build` složky.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="c8a1d-121">Instalace a odinstalace skripty, které podporují projektů pomocí `packages.config` jsou umístěny v `tools`.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="c8a1d-122">Také Všimněte si, že vzhledem k tomu, že tento balíček nemá žádné požadavky specifické pro platformu `platform` složky je vynechán.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="c8a1d-123">Formát cesty analyzátory</span><span class="sxs-lookup"><span data-stu-id="c8a1d-123">Analyzers path format</span></span>

<span data-ttu-id="c8a1d-124">Použití `analyzers` složka je podobná používá pro [cílové rozhraní](../create-packages/supporting-multiple-target-frameworks.md), s výjimkou specifikátory v cestě popisují vývoj hostitele závislosti místo čase vytvoření buildu.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="c8a1d-125">Obecný formát vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="c8a1d-125">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}}/{analyzer_name}.dll

- <span data-ttu-id="c8a1d-126">**framework_name**: *volitelné* rozhraní API útoku na rozhraní .NET Framework, která obsahují knihovny DLL je potřeba spustit.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-126">**framework_name**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="c8a1d-127">`dotnet` protože Roslyn je jenom hostitele, který můžete spustit analyzátorů je v současné době jedinou platnou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="c8a1d-128">Pokud není zadaný žádný cíl, knihovny DLL se předpokládá, že pokud chcete použít pro *všechny* cíle.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="c8a1d-129">**supported_language**: jazyk, pro kterou knihovnu DLL platí, jeden z `cs` (C#) a `vb` (Visual Basic), a `fs` (F #).</span><span class="sxs-lookup"><span data-stu-id="c8a1d-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="c8a1d-130">Jazyk označuje, že nástroje analyzer by měly být načteny pouze pro projekt pomocí daného jazyka.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="c8a1d-131">Pokud je zadán žádný jazyk, pak DLL se předpokládá, že pokud chcete použít pro *všechny* jazyky, které podporují analyzátorů.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-131">If no language is specified then DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="c8a1d-132">**analyzer_name**: Určuje knihovny DLL analyzéru.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="c8a1d-133">Pokud potřebujete další soubory nad rámec knihovny DLL, musí být zahrnuty v souborech cíle nebo vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="c8a1d-134">Instalace a odinstalace skripty</span><span class="sxs-lookup"><span data-stu-id="c8a1d-134">Install and uninstall scripts</span></span>

<span data-ttu-id="c8a1d-135">Pokud je projekt uživatele pomocí `packages.config`, MSBuild skript, který převezme nástroje analyzer nepřejde do play, proto byste měli `install.ps1` a `uninstall.ps1` v `tools` složku s obsahem, které jsou popsány níže.</span><span class="sxs-lookup"><span data-stu-id="c8a1d-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="c8a1d-136">**obsah souboru Install.ps1**</span><span class="sxs-lookup"><span data-stu-id="c8a1d-136">**install.ps1 file contents**</span></span>

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


<span data-ttu-id="c8a1d-137">**obsah souboru Uninstall.ps1**</span><span class="sxs-lookup"><span data-stu-id="c8a1d-137">**uninstall.ps1 file contents**</span></span>

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
