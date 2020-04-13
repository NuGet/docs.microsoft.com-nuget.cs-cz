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
# <a name="analyzer-nuget-formats"></a>Analyzátor NuGet formáty

Platforma kompilátoru .NET (označovaná také jako "Roslyn") umožňuje vývojářům vytvářet [analyzátory,](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) které zkoumají strom syntaxe a sémantiku kódu při jeho zápisu. To poskytuje vývojářům způsob, jak vytvořit nástroje pro analýzu specifické pro doménu, jako jsou ty, které by pomohly řídit použití konkrétního rozhraní API nebo knihovny. Více informací najdete na wiki [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub. Viz také [článek, Použijte Roslyn napsat Live Analyzátor kódu pro vaše rozhraní API](https://msdn.microsoft.com/magazine/dn879356.aspx) v MSDN Magazine.

Analyzátory samy o sobě jsou obvykle zabaleny a distribuovány jako součást nuget balíčky, které implementují rozhraní API nebo knihovny v otázce.

Dobrý příklad naleznete v balíčku [System.Runtime.Analyzers,](https://www.nuget.org/packages/System.Runtime.Analyzers) který má následující obsah:

- analyzátory\dotnet\System.Runtime.Analyzers.dll
- analyzátory\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzátory\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- nástroje\install.ps1
- nástroje\uninstall.ps1

Jak můžete vidět, umístíte knihovny DLL `analyzers` analyzátoru do složky v balíčku.

Rekvizity soubory, které jsou zahrnuty zakázat starší FxCop pravidla ve `build` prospěch implementace analyzátoru, jsou umístěny ve složce.

Instalace a odinstalace skriptů, `packages.config` které `tools`podporují projekty pomocí jsou umístěny v aplikaci .

Všimněte si také, že vzhledem k `platform` tomu, že tento balíček nemá žádné požadavky specifické pro platformu, složka je vynechána.


## <a name="analyzers-path-format"></a>Formát cesty analyzátorů

Použití `analyzers` složky je podobné jako u [cílových architektur](../create-packages/supporting-multiple-target-frameworks.md), s výjimkou specifikátorů v cestě popisují závislosti hostitele vývoje namísto sestavení. Obecný formát je následující:

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- **framework_name** a **verze**: *volitelná* plocha rozhraní API rozhraní .NET Framework, kterou musí spustit obsažené knihovny DLL. `dotnet`je v současné době jedinou platnou hodnotu, protože Roslyn je jediný hostitel, který může spustit analyzátory. Pokud není zadán žádný cíl, předpokládá se, že knihovny DLL se použijí na *všechny* cíle.
- **supported_language**: jazyk, pro který se vztahuje `cs` dll, `vb` jeden z (C#) a (Visual Basic) a `fs` (F#). Jazyk označuje, že analyzátor by měl být načten pouze pro projekt používající tento jazyk. Pokud není zadán žádný jazyk, předpokládá se, že dll se vztahuje na *všechny* jazyky, které podporují analyzátory.
- **analyzer_name**: určuje knihovny DLL analyzátoru. Pokud potřebujete další soubory nad rámec knihoven DLL, musí být zahrnuty prostřednictvím souborů cílů nebo vlastností.


## <a name="install-and-uninstall-scripts"></a>Instalace a odinstalace skriptů

Pokud projekt uživatele `packages.config`používá , skript MSBuild, který vyzvedne analyzátor nevstoupí do `install.ps1` hry, takže byste měli umístit a `uninstall.ps1` ve `tools` složce s obsahem, které jsou popsány níže.

**install.ps1 obsah souboru**

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


**odinstalovat soubor PS1**

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
