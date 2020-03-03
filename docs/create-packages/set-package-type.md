---
title: Nastavení typu balíčku NuGet
description: Popisuje typy balíčků k označení zamýšleného použití balíčku.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230821"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="30372-103">Nastavení typu balíčku NuGet</span><span class="sxs-lookup"><span data-stu-id="30372-103">Set a NuGet package type</span></span>

<span data-ttu-id="30372-104">S NuGet 3.5 + můžete balíčky označit pomocí konkrétního *typu balíčku* , aby označovali zamýšlené použití.</span><span class="sxs-lookup"><span data-stu-id="30372-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="30372-105">Balíčky, které nejsou označeny typem, včetně všech balíčků vytvořených v dřívějších verzích NuGet, jsou ve výchozím nastavení typu `Dependency`.</span><span class="sxs-lookup"><span data-stu-id="30372-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="30372-106">balíčky typů `Dependency` přidávají do knihoven a aplikací prostředky run-time a můžou být nainstalované v jakémkoli typu projektu (za předpokladu, že jsou kompatibilní).</span><span class="sxs-lookup"><span data-stu-id="30372-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="30372-107">balíčky typů `DotnetTool` jsou rozšířením rozhraní příkazového řádku [dotnet](/dotnet/articles/core/tools/index) a jsou vyvolána z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="30372-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="30372-108">Takové balíčky lze nainstalovat pouze v projektech .NET Core a nemají žádný vliv na operace obnovení.</span><span class="sxs-lookup"><span data-stu-id="30372-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="30372-109">Další podrobnosti o těchto rozšířeních pro jednotlivé projekty jsou k dispozici v dokumentaci [rozšiřitelnosti .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) .</span><span class="sxs-lookup"><span data-stu-id="30372-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="30372-110">balíčky typů `Template` poskytují [vlastní šablony](/dotnet/core/tools/custom-templates) , které lze použít k vytvoření souborů nebo projektů, jako je aplikace, služby, nástroje nebo knihovna tříd.</span><span class="sxs-lookup"><span data-stu-id="30372-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="30372-111">Balíčky vlastních typů používají libovolný identifikátor typu, který odpovídá stejným pravidlům formátu jako ID balíčků.</span><span class="sxs-lookup"><span data-stu-id="30372-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="30372-112">Správce balíčků NuGet v aplikaci Visual Studio však nerozpoznal jiný typ než `Dependency` a `DotnetTool`.</span><span class="sxs-lookup"><span data-stu-id="30372-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="30372-113">Typy balíčků jsou nastaveny v souboru `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="30372-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="30372-114">Je nejvhodnější pro zpětnou *kompatibilitu, aby neexplicitně* nastavila typ `Dependency` a místo toho se spoléhá na NuGet za předpokladu, že není zadán žádný typ.</span><span class="sxs-lookup"><span data-stu-id="30372-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="30372-115">`.nuspec`: Určete typ balíčku v rámci uzlu `packageTypes\packageType` pod prvkem `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="30372-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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
