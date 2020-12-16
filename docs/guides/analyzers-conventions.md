---
title: Formáty .NET Compiler Platform Analyzer pro NuGet
description: Konvence pro analyzátory .NET, které jsou zabaleny a distribuovány pomocí balíčků NuGet, které implementují rozhraní API nebo knihovny.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: f1e9bb96fc7acc73ec37cebcdc8015081fafb307
ms.sourcegitcommit: 650c08f8bc3d48dfd206a111e5e2aaca3001f569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/15/2020
ms.locfileid: "97523413"
---
# <a name="analyzer-nuget-formats"></a>Formáty NuGet analyzátoru

.NET Compiler Platform (označované také jako "Roslyn") umožňuje vývojářům vytvářet [analyzátory](https://github.com/dotnet/roslyn/blob/master/docs/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix.md) , které zkoumají strom syntaxe a sémantiku kódu při zápisu. To poskytuje vývojářům možnost vytvářet nástroje pro analýzu specifické pro doménu, jako jsou ty, které by pomohly s použitím konkrétního rozhraní API nebo knihovny. Další informace najdete na wikiwebu [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub. Přečtěte si také článek [použití Roslyn k zápisu živého analyzátoru kódu pro vaše rozhraní API](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api) na webu MSDN Magazine.

Samotné analyzátory jsou obvykle zabaleny a distribuovány jako součást balíčků NuGet, které implementují příslušné rozhraní API nebo knihovny.

Dobrý příklad naleznete v balíčku [System. Runtime. analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) , který má následující obsah:

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\install.ps1
- tools\uninstall.ps1

Jak vidíte, umístěte knihovny DLL analyzátoru do `analyzers` složky v balíčku.

Soubory props, které jsou zahrnuty pro zakázání starších pravidel FxCop ve prospěch implementace analyzátoru, jsou umístěny do `build` složky.

Instalace a odinstalace skriptů podporujících projekty pomocí `packages.config` jsou umístěny v `tools` .

Všimněte si také, že vzhledem k tomu, že tento balíček nemá žádné požadavky specifické pro platformu, `platform` je tato složka vynechána.


## <a name="analyzers-path-format"></a>Formát cesty analyzátorů

Použití `analyzers` složky je podobné jako u [cílových rozhraní](../create-packages/supporting-multiple-target-frameworks.md), s výjimkou specifikátorů v cestě popisují závislosti vývojového hostitele namísto doby sestavení. Obecný formát je následující:

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- **framework_name** a **verze**: *volitelná* oblast rozhraní API .NET Framework, kterou obsažené knihovny DLL musí spustit. `dotnet` je v současné době jediná platná hodnota, protože Roslyn je jediný hostitel, který může spustit analyzátory. Pokud není zadán žádný cíl, považují se knihovny DLL za použití na *všechny* cíle.
- **supported_language**: jazyk, pro který se knihovna DLL používá, jedna z `cs` (C#) a `vb` (Visual Basic) a `fs` (F #). Jazyk označuje, že analyzátor má být načten pouze pro projekt, který používá daný jazyk. Pokud není zadán žádný jazyk, předpokládá se, že se knihovna DLL použije pro *všechny* jazyky, které podporují analyzátory.
- **analyzer_name**: Určuje knihovny DLL analyzátoru. Pokud potřebujete další soubory kromě knihoven DLL, musí být zahrnuty prostřednictvím cílů nebo souborů vlastností.


## <a name="install-and-uninstall-scripts"></a>Instalace a odinstalace skriptů

Pokud projekt uživatele používá `packages.config` , skript MSBuild, který vybírá analyzátor, nepřichází do hry, takže byste měli umístit `install.ps1` `uninstall.ps1` `tools` složku s obsahem, který je popsán níže.

**install.ps1 obsahu souboru**

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


**uninstall.ps1 obsahu souboru**

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
