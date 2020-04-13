---
title: Nastavení typu balíčku NuGet
description: Popisuje typy balíčků označující zamýšlené použití balíčku.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230821"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="47ed8-103">Nastavení typu balíčku NuGet</span><span class="sxs-lookup"><span data-stu-id="47ed8-103">Set a NuGet package type</span></span>

<span data-ttu-id="47ed8-104">S NuGet 3.5+, balíčky mohou být označeny určitým *typem balíčku* k označení jeho zamýšlené použití.</span><span class="sxs-lookup"><span data-stu-id="47ed8-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="47ed8-105">Balíčky, které nejsou označeny typem, včetně všech balíčků vytvořených s dřívějšími verzemi NuGet, výchozí `Dependency` typ.</span><span class="sxs-lookup"><span data-stu-id="47ed8-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="47ed8-106">`Dependency`typy balíčků přidat sestavení nebo run-time datové zdroje do knihoven a aplikací a lze nainstalovat v libovolném typu projektu (za předpokladu, že jsou kompatibilní).</span><span class="sxs-lookup"><span data-stu-id="47ed8-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="47ed8-107">`DotnetTool`typy balíčků jsou rozšíření [dotnet CLI](/dotnet/articles/core/tools/index) a jsou vyvolány z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="47ed8-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="47ed8-108">Tyto balíčky lze nainstalovat pouze v projektech .NET Core a nemají žádný vliv na operace obnovení.</span><span class="sxs-lookup"><span data-stu-id="47ed8-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="47ed8-109">Další podrobnosti o těchto rozšíření chod projektu jsou k dispozici v dokumentaci [rozšiřitelnosti jádra .NET.](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)</span><span class="sxs-lookup"><span data-stu-id="47ed8-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="47ed8-110">`Template`balíčky typů poskytují [vlastní šablony,](/dotnet/core/tools/custom-templates) které lze použít k vytvoření souborů nebo projektů, jako je aplikace, služba, nástroj nebo knihovna tříd.</span><span class="sxs-lookup"><span data-stu-id="47ed8-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="47ed8-111">Balíčky vlastních typů používají libovolný identifikátor typu, který odpovídá stejným pravidlům formátu jako ID balíčků.</span><span class="sxs-lookup"><span data-stu-id="47ed8-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="47ed8-112">Všechny typy `Dependency` než `DotnetTool`a , však nejsou rozpoznány NuGet Package Manager v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="47ed8-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="47ed8-113">Typy balíčků jsou `.nuspec` nastaveny v souboru.</span><span class="sxs-lookup"><span data-stu-id="47ed8-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="47ed8-114">Je nejvhodnější pro zpětnou *not* kompatibilitu není `Dependency` explicitně nastavit typ a místo toho spoléhat na NuGet za předpokladu, že tento typ, když není zadán žádný typ.</span><span class="sxs-lookup"><span data-stu-id="47ed8-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="47ed8-115">`.nuspec`: Označte typ `packageTypes\packageType` balíčku v `<metadata>` uzlu pod elementem:</span><span class="sxs-lookup"><span data-stu-id="47ed8-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
