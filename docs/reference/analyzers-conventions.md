---
title: .NET kompilátoru platformy analyzátor formáty pro NuGet
description: Konvence pro .NET analyzátory, které jsou zabaleny a distribuovat s balíčky NuGet, které implementují rozhraní API nebo knihovny.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0a8db9f6c55b7e79f9b338119e0b3ac6cb7a1e35
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324796"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="02075-103">Analyzátor NuGet formáty</span><span class="sxs-lookup"><span data-stu-id="02075-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="02075-104">.NET Compiler Platform (označované také jako "Roslyn") umožňuje vývojářům vytvářet [analyzátory](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) , zkontrolujte stromu syntaxe a sémantiky kódu jako se zápisem.</span><span class="sxs-lookup"><span data-stu-id="02075-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="02075-105">To poskytuje vývojářům způsob, jak vytvořit specifického pro doménu analytické nástroje, jako jsou například ty, které by pomohl příručka k užívání konkrétní rozhraní API nebo knihovny.</span><span class="sxs-lookup"><span data-stu-id="02075-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="02075-106">Další informace najdete v [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) Wiki úložiště GitHub.</span><span class="sxs-lookup"><span data-stu-id="02075-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="02075-107">Také naleznete v článku [Roslyn použít k zápisu Live Code Analyzer pro vaše rozhraní API](https://msdn.microsoft.com/magazine/dn879356.aspx) v MSDN Magazine.</span><span class="sxs-lookup"><span data-stu-id="02075-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="02075-108">Analyzátory samotné jsou obvykle zabalit a distribuovat jako součást balíčků NuGet, které implementují rozhraní API nebo knihovny dotyčný.</span><span class="sxs-lookup"><span data-stu-id="02075-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="02075-109">Dobrým příkladem, najdete v článku [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) balíček, který má následující obsah:</span><span class="sxs-lookup"><span data-stu-id="02075-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="02075-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="02075-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="02075-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="02075-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="02075-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="02075-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="02075-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="02075-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="02075-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="02075-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="02075-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="02075-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="02075-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="02075-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="02075-117">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="02075-117">tools\install.ps1</span></span>
- <span data-ttu-id="02075-118">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="02075-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="02075-119">Jak je vidět, umístíte analyzátor knihoven DLL do `analyzers` složky v balíčku.</span><span class="sxs-lookup"><span data-stu-id="02075-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="02075-120">Soubory vlastností, které jsou součástí zakázat zastaralá pravidla FxCop ve prospěch implementaci analyzátoru, jsou umístěny v `build` složky.</span><span class="sxs-lookup"><span data-stu-id="02075-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="02075-121">Instalace a odinstalace skripty, které podporují projektů s použitím `packages.config` jsou umístěny v `tools`.</span><span class="sxs-lookup"><span data-stu-id="02075-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="02075-122">Všimněte si také, protože tento balíček nemá žádné požadavky na specifické pro platformu `platform` složky je vynechán.</span><span class="sxs-lookup"><span data-stu-id="02075-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="02075-123">Formát cesty analyzátory</span><span class="sxs-lookup"><span data-stu-id="02075-123">Analyzers path format</span></span>

<span data-ttu-id="02075-124">Použití `analyzers` složka je podobný, který používá pro [platforem](../create-packages/supporting-multiple-target-frameworks.md), s výjimkou popisují specifikátory v cestě vývoj hostitele mdildll čas sestavení.</span><span class="sxs-lookup"><span data-stu-id="02075-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="02075-125">Obecný formát je následující:</span><span class="sxs-lookup"><span data-stu-id="02075-125">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- <span data-ttu-id="02075-126">**framework_name**: *volitelné* svrchní oblasti rozhraní API z rozhraní .NET Framework, omezením knihovny DLL je potřeba spustit.</span><span class="sxs-lookup"><span data-stu-id="02075-126">**framework_name**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="02075-127">`dotnet` protože je pouze hostitele, který můžete spustit analyzátory Roslyn je v současné době jediná platná hodnota.</span><span class="sxs-lookup"><span data-stu-id="02075-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="02075-128">Pokud není zadán žádný cíl, knihovny DLL se předpokládá, že pokud chcete použít pro *všechny* cíle.</span><span class="sxs-lookup"><span data-stu-id="02075-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="02075-129">**supported_language**: jazyk, pro který knihovnu DLL se vztahuje, jeden z `cs` (C#) a `vb` (Visual Basic), a `fs` (F#).</span><span class="sxs-lookup"><span data-stu-id="02075-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="02075-130">Jazyk určuje, že analyzátor by měly být načteny pouze pro projekt pomocí tohoto jazyka.</span><span class="sxs-lookup"><span data-stu-id="02075-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="02075-131">Pokud je zadán žádný jazyk, pak knihovnu DLL se předpokládá, že pokud chcete použít pro *všechny* jazyky, které podporují analyzátory.</span><span class="sxs-lookup"><span data-stu-id="02075-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="02075-132">**analyzer_name**: Určuje DLL analyzátor.</span><span class="sxs-lookup"><span data-stu-id="02075-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="02075-133">Pokud potřebujete další soubory nad rámec knihovny DLL, musí být zahrnuty do cíle a vlastnosti souborů.</span><span class="sxs-lookup"><span data-stu-id="02075-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="02075-134">Instalace a odinstalace skriptů</span><span class="sxs-lookup"><span data-stu-id="02075-134">Install and uninstall scripts</span></span>

<span data-ttu-id="02075-135">Pokud je projekt uživatele pomocí `packages.config`, MSBuild skript, který převezme analyzátor nepřejde do hry, takže byste měli umístit `install.ps1` a `uninstall.ps1` v `tools` složku s obsahem, které jsou popsány níže.</span><span class="sxs-lookup"><span data-stu-id="02075-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="02075-136">**obsah souboru Install.ps1**</span><span class="sxs-lookup"><span data-stu-id="02075-136">**install.ps1 file contents**</span></span>

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


<span data-ttu-id="02075-137">**obsah souboru Uninstall.ps1**</span><span class="sxs-lookup"><span data-stu-id="02075-137">**uninstall.ps1 file contents**</span></span>

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
