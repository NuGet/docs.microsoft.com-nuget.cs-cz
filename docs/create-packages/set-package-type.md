---
title: Nastavení typu balíčku NuGet
description: Popisuje typy balíčků k označení zamýšleného použití balíčku.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 22e8ac2e9e2086a1280c5b0c3be8a032b7998b36
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036913"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="a2f58-103">Nastavení typu balíčku NuGet</span><span class="sxs-lookup"><span data-stu-id="a2f58-103">Set a NuGet package type</span></span>

<span data-ttu-id="a2f58-104">S NuGet 3.5 + můžete balíčky označit pomocí konkrétního *typu balíčku* , aby označovali zamýšlené použití.</span><span class="sxs-lookup"><span data-stu-id="a2f58-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="a2f58-105">Balíčky, které nejsou označeny typem, včetně všech balíčků vytvořených v dřívějších verzích NuGet, jsou ve výchozím nastavení typu `Dependency`.</span><span class="sxs-lookup"><span data-stu-id="a2f58-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="a2f58-106">balíčky typů `Dependency` přidávají do knihoven a aplikací prostředky run-time a můžou být nainstalované v jakémkoli typu projektu (za předpokladu, že jsou kompatibilní).</span><span class="sxs-lookup"><span data-stu-id="a2f58-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="a2f58-107">balíčky typů `DotnetTool` jsou rozšířením rozhraní příkazového řádku [dotnet](/dotnet/articles/core/tools/index) a jsou vyvolána z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="a2f58-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="a2f58-108">Takové balíčky lze nainstalovat pouze v projektech .NET Core a nemají žádný vliv na operace obnovení.</span><span class="sxs-lookup"><span data-stu-id="a2f58-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="a2f58-109">Další podrobnosti o těchto rozšířeních pro jednotlivé projekty jsou k dispozici v dokumentaci [rozšiřitelnosti .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) .</span><span class="sxs-lookup"><span data-stu-id="a2f58-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="a2f58-110">balíčky typů `Template` poskytují [vlastní šablony](/dotnet/core/tools/custom-templates) , které lze použít k vytvoření souborů nebo projektů, jako je aplikace, služby, nástroje nebo knihovna tříd.</span><span class="sxs-lookup"><span data-stu-id="a2f58-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="a2f58-111">Balíčky vlastních typů používají libovolný identifikátor typu, který odpovídá stejným pravidlům formátu jako ID balíčků.</span><span class="sxs-lookup"><span data-stu-id="a2f58-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="a2f58-112">Správce balíčků NuGet v aplikaci Visual Studio však nerozpoznal jiný typ než `Dependency` a `DotnetTool`.</span><span class="sxs-lookup"><span data-stu-id="a2f58-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="a2f58-113">Typy balíčků jsou nastaveny v souboru `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="a2f58-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="a2f58-114">Je nejvhodnější pro zpětnou *kompatibilitu, aby neexplicitně* nastavila typ `Dependency` a místo toho se spoléhá na NuGet za předpokladu, že není zadán žádný typ.</span><span class="sxs-lookup"><span data-stu-id="a2f58-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="a2f58-115">`.nuspec`: Určete typ balíčku v rámci uzlu `packageTypes\packageType` pod prvkem `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="a2f58-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
