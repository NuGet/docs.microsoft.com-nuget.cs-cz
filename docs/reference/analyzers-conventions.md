---
title: .NET kompilátoru platformy analyzátor formáty pro NuGet
description: Konvence pro .NET analyzátory, které jsou zabaleny a distribuovat s balíčky NuGet, které implementují rozhraní API nebo knihovny.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: a5ccbba5fbc189eb59acfdeb86a4a03dcf907a9a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547628"
---
# <a name="analyzer-nuget-formats"></a>Analyzátor NuGet formáty

.NET Compiler Platform (označované také jako "Roslyn") umožňují vývojářům vytvářet [analyzátory](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) , zkontrolujte stromu syntaxe a sémantiky kódu jako se zápisem. To poskytuje vývojářům způsob, jak vytvořit a nástroji pro analýzu specifického pro doménu, například ty, které by pomohl příručka k užívání konkrétní rozhraní API nebo knihovny. Další informace najdete v [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) Wiki úložiště GitHub. Také naleznete v článku [Roslyn použít k zápisu Live Code Analyzer pro vaše rozhraní API](https://msdn.microsoft.com/magazine/dn879356.aspx) v MSDN Magazine.

Analyzátory samotné jsou obvykle zabalit a distribuovat jako součást balíčků NuGet, které implementují rozhraní API nebo knihovny dotyčný.

Dobrým příkladem, najdete v článku [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) balíček, který má následující obsah:

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\install.ps1
- tools\uninstall.ps1

Jak je vidět, umístíte analyzátor knihoven DLL do `analyzers` složky v balíčku.

Soubory vlastností, které jsou součástí zakázat zastaralá pravidla FxCop ve prospěch implementaci analyzátoru, jsou umístěny v `build` složky.

Instalace a odinstalace skripty, které podporují projektů s použitím `packages.config` jsou umístěny v `tools`.

Všimněte si také, protože tento balíček nemá žádné požadavky na specifické pro platformu `platform` složky je vynechán.


## <a name="analyzers-path-format"></a>Formát cesty analyzátory

Použití `analyzers` složka je podobný, který používá pro [platforem](../create-packages/supporting-multiple-target-frameworks.md), s výjimkou popisují specifikátory v cestě vývoj hostitele mdildll čas sestavení. Obecný formát je následující:

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- **framework_name**: *volitelné* svrchní oblasti rozhraní API z rozhraní .NET Framework, omezením knihovny DLL je potřeba spustit. `dotnet` protože je pouze hostitele, který můžete spustit analyzátory Roslyn je v současné době jediná platná hodnota. Pokud není zadán žádný cíl, knihovny DLL se předpokládá, že pokud chcete použít pro *všechny* cíle.
- **supported_language**: jazyk, pro který knihovnu DLL se vztahuje, jeden z `cs` (C#) a `vb` (Visual Basic), a `fs` (F #). Jazyk určuje, že analyzátor by měly být načteny pouze pro projekt pomocí tohoto jazyka. Pokud je zadán žádný jazyk, pak knihovny DLL se předpokládá, že pokud chcete použít pro *všechny* jazyky, které podporují analyzátory.
- **analyzer_name**: Určuje DLL analyzátor. Pokud potřebujete další soubory nad rámec knihovny DLL, musí být zahrnuty do cíle a vlastnosti souborů.


## <a name="install-and-uninstall-scripts"></a>Instalace a odinstalace skriptů

Pokud je projekt uživatele pomocí `packages.config`, MSBuild skript, který převezme analyzátor nepřejde do hry, takže byste měli `install.ps1` a `uninstall.ps1` v `tools` složku s obsahem, které jsou popsány níže.

**obsah souboru Install.ps1**

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


**obsah souboru Uninstall.ps1**

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
