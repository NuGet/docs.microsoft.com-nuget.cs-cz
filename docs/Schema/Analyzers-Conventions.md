---
title: "Pro NuGet formátů analyzátor platformy .NET kompilátoru | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Konvence pro analyzátory .NET, které se zabalí a distribuovat s balíčky NuGet, které implementují rozhraní API nebo knihovny."
keywords: "Konvence analyzátor NuGet, .NET analyzátorů, NuGet a kompilátoru platformy .NET, NuGet a Roslyn"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e44cfa609c14422d50769e512108844cbd2f96a4
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/31/2018
---
# <a name="analyzer-nuget-formats"></a>Analyzátor NuGet formáty

Kompilátoru platformu .NET (také označované jako "Roslyn") umožňují vývojářům vytvářet [analyzátorů] (https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix), podívejte se na strom syntaxe a sémantiku kódu se zapsané. To poskytuje vývojářům způsob, jak vytvořit a specifické pro doménu analytické nástroje, jako jsou ty, které pomohou průvodce použít konkrétní rozhraní API nebo knihovny. Další informace najdete na [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) wiki Githubu. Také najdete v článku [Roslyn použití k zápisu Live analyzátor kódu pro vaše rozhraní API](https://msdn.microsoft.com/magazine/dn879356.aspx) v časopise MSDN.

Analyzátory sami jsou obvykle zabalené a distribuovat jako součást balíčky NuGet, které implementují rozhraní API nebo knihovny nejistá.

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

Jak vidíte, umístíte analyzátor knihoven DLL do `analyzers` složky v balíčku.

Soubory props, které jsou součástí zakázat zastaralá pravidla FxCop považuje implementace analyzátor, jsou umístěny v `build` složky.

Instalace a odinstalace skripty, které podporují projektů pomocí `packages.config` jsou umístěny v `tools`.

Také Všimněte si, že vzhledem k tomu, že tento balíček nemá žádné požadavky specifické pro platformu `platform` složky je vynechán.


## <a name="analyzers-path-format"></a>Formát cesty analyzátory

Použití `analyzers` složka je podobná používá pro [cílové rozhraní](../create-packages/supporting-multiple-target-frameworks.md), s výjimkou specifikátory v cestě popisují vývoj hostitele závislosti místo čase vytvoření buildu. Obecný formát vypadá takto:

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}}/{analyzer_name}.dll

- **framework_name**: *volitelné* rozhraní API útoku na rozhraní .NET Framework, která obsahují knihovny DLL je potřeba spustit. `dotnet`protože Roslyn je jenom hostitele, který můžete spustit analyzátorů je v současné době jedinou platnou hodnotou. Pokud není zadaný žádný cíl, knihovny DLL se předpokládá, že pokud chcete použít pro *všechny* cíle.
- **supported_language**: jazyk, pro kterou knihovnu DLL platí, jeden z `cs` (C#) a `vb` (Visual Basic), a `fs` (F #). Jazyk označuje, že nástroje analyzer by měly být načteny pouze pro projekt pomocí daného jazyka. Pokud je zadán žádný jazyk, pak DLL se předpokládá, že pokud chcete použít pro *všechny* jazyky, které podporují analyzátorů.
- **analyzer_name**: Určuje knihovny DLL analyzéru. Pokud potřebujete další soubory nad rámec knihovny DLL, musí být zahrnuty v souborech cíle nebo vlastnosti.


## <a name="install-and-uninstall-scripts"></a>Instalace a odinstalace skripty

Pokud je projekt uživatele pomocí `packages.config`, MSBuild skript, který převezme nástroje analyzer nepřejde do play, proto byste měli `install.ps1` a `uninstall.ps1` v `tools` složku s obsahem, které jsou popsány níže.

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
