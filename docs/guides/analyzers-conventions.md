---
title: Formáty .NET Compiler Platform Analyzer pro NuGet
description: Konvence pro analyzátory .NET, které jsou zabaleny a distribuovány pomocí balíčků NuGet, které implementují rozhraní API nebo knihovny.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 63880b6b9bbfe6aac9cc6419d6a972062eea3495
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774125"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="9cdc2-103">Formáty NuGet analyzátoru</span><span class="sxs-lookup"><span data-stu-id="9cdc2-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="9cdc2-104">.NET Compiler Platform (označované také jako "Roslyn") umožňuje vývojářům vytvářet [analyzátory](https://github.com/dotnet/roslyn/blob/master/docs/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix.md) , které zkoumají strom syntaxe a sémantiku kódu při zápisu.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/blob/master/docs/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix.md) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="9cdc2-105">To poskytuje vývojářům možnost vytvářet nástroje pro analýzu specifické pro doménu, jako jsou ty, které by pomohly s použitím konkrétního rozhraní API nebo knihovny.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="9cdc2-106">Další informace najdete na wikiwebu [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="9cdc2-107">Přečtěte si také článek [použití Roslyn k zápisu živého analyzátoru kódu pro vaše rozhraní API](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api) na webu MSDN Magazine.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api) in MSDN Magazine.</span></span>

<span data-ttu-id="9cdc2-108">Samotné analyzátory jsou obvykle zabaleny a distribuovány jako součást balíčků NuGet, které implementují příslušné rozhraní API nebo knihovny.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="9cdc2-109">Dobrý příklad naleznete v balíčku [System. Runtime. analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) , který má následující obsah:</span><span class="sxs-lookup"><span data-stu-id="9cdc2-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="9cdc2-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="9cdc2-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="9cdc2-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="9cdc2-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="9cdc2-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="9cdc2-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="9cdc2-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="9cdc2-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="9cdc2-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="9cdc2-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="9cdc2-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="9cdc2-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="9cdc2-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="9cdc2-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="9cdc2-117">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="9cdc2-117">tools\install.ps1</span></span>
- <span data-ttu-id="9cdc2-118">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="9cdc2-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="9cdc2-119">Jak vidíte, umístěte knihovny DLL analyzátoru do `analyzers` složky v balíčku.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="9cdc2-120">Soubory props, které jsou zahrnuty pro zakázání starších pravidel FxCop ve prospěch implementace analyzátoru, jsou umístěny do `build` složky.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="9cdc2-121">Instalace a odinstalace skriptů podporujících projekty pomocí `packages.config` jsou umístěny v `tools` .</span><span class="sxs-lookup"><span data-stu-id="9cdc2-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="9cdc2-122">Všimněte si také, že vzhledem k tomu, že tento balíček nemá žádné požadavky specifické pro platformu, `platform` je tato složka vynechána.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="9cdc2-123">Formát cesty analyzátorů</span><span class="sxs-lookup"><span data-stu-id="9cdc2-123">Analyzers path format</span></span>

<span data-ttu-id="9cdc2-124">Použití `analyzers` složky je podobné jako u [cílových rozhraní](../create-packages/supporting-multiple-target-frameworks.md), s výjimkou specifikátorů v cestě popisují závislosti vývojového hostitele namísto doby sestavení.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="9cdc2-125">Obecný formát je následující:</span><span class="sxs-lookup"><span data-stu-id="9cdc2-125">The general format is as follows:</span></span>

```
$/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll
```

- <span data-ttu-id="9cdc2-126">**framework_name** a **verze**: *volitelná* oblast rozhraní API .NET Framework, kterou obsažené knihovny DLL musí spustit.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-126">**framework_name** and **version**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="9cdc2-127">`dotnet` je v současné době jediná platná hodnota, protože Roslyn je jediný hostitel, který může spustit analyzátory.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="9cdc2-128">Pokud není zadán žádný cíl, považují se knihovny DLL za použití na *všechny* cíle.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="9cdc2-129">**supported_language**: jazyk, pro který se knihovna DLL používá, jedna z `cs` (C#) a `vb` (Visual Basic) a `fs` (F #).</span><span class="sxs-lookup"><span data-stu-id="9cdc2-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="9cdc2-130">Jazyk označuje, že analyzátor má být načten pouze pro projekt, který používá daný jazyk.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="9cdc2-131">Pokud není zadán žádný jazyk, předpokládá se, že se knihovna DLL použije pro *všechny* jazyky, které podporují analyzátory.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="9cdc2-132">**analyzer_name**: Určuje knihovny DLL analyzátoru.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="9cdc2-133">Pokud potřebujete další soubory kromě knihoven DLL, musí být zahrnuty prostřednictvím cílů nebo souborů vlastností.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="9cdc2-134">Instalace a odinstalace skriptů</span><span class="sxs-lookup"><span data-stu-id="9cdc2-134">Install and uninstall scripts</span></span>

<span data-ttu-id="9cdc2-135">Pokud projekt uživatele používá `packages.config` , skript MSBuild, který vybírá analyzátor, nepřichází do hry, takže byste měli umístit `install.ps1` `uninstall.ps1` `tools` složku s obsahem, který je popsán níže.</span><span class="sxs-lookup"><span data-stu-id="9cdc2-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="9cdc2-136">**install.ps1 obsahu souboru**</span><span class="sxs-lookup"><span data-stu-id="9cdc2-136">**install.ps1 file contents**</span></span>

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


<span data-ttu-id="9cdc2-137">**uninstall.ps1 obsahu souboru**</span><span class="sxs-lookup"><span data-stu-id="9cdc2-137">**uninstall.ps1 file contents**</span></span>

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
