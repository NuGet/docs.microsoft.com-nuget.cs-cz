---
title: Nastavit typ balíčku NuGet
description: Popisuje typy balíčků k označení zamýšlené použití souboru balíčku.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 8a3ba6af19125b75af17cab8c093e89485e20324
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843533"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="462a0-103">Nastavit typ balíčku NuGet</span><span class="sxs-lookup"><span data-stu-id="462a0-103">Set a NuGet package type</span></span>

<span data-ttu-id="462a0-104">Nuget 3.5 +, může být označený balíčky s konkrétním *typ balíčku* označující jeho zamýšlené použití.</span><span class="sxs-lookup"><span data-stu-id="462a0-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="462a0-105">Balíčky není označena jako s typem, včetně všech balíčků, které jsou vytvořené pomocí starší verze balíčku nuget, ve výchozím nastavení `Dependency` typu.</span><span class="sxs-lookup"><span data-stu-id="462a0-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="462a0-106">`Dependency` balíčky typ sestavení nebo runtime prostředky přidat do knihovny a aplikace a může být nainstalován v libovolným typem projektu (za předpokladu, že jsou kompatibilní).</span><span class="sxs-lookup"><span data-stu-id="462a0-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="462a0-107">`DotnetCliTool` Typ balíčky jsou rozšíření [rozhraní příkazového řádku dotnet](/dotnet/articles/core/tools/index) a jsou vyvolány z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="462a0-107">`DotnetCliTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="462a0-108">Tyto balíčky můžete nainstalovat jenom v projektech .NET Core a nemají žádný vliv na operace obnovení.</span><span class="sxs-lookup"><span data-stu-id="462a0-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="462a0-109">Další podrobnosti o těchto rozšířeních jednotlivých projektů jsou dostupné v [rozšiřitelnost .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="462a0-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="462a0-110">Vlastní typ balíčky pomocí libovolného typu identifikátor, který odpovídá stejná pravidla formát jako ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="462a0-110">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="462a0-111">Jakýkoli typ jiný než `Dependency` a `DotnetCliTool`, ale nejsou rozpoznány v aplikaci Správce balíčků NuGet v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="462a0-111">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="462a0-112">Typy balíčků jsou nastaveny `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="462a0-112">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="462a0-113">Je nejvhodnější pro zpětnou kompatibilitu s *není* explicitně nastaveno `Dependency` zadejte a místo toho přináší setrvávání u NuGet tohoto typu, pokud žádný typ za předpokladu, že je zadán.</span><span class="sxs-lookup"><span data-stu-id="462a0-113">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="462a0-114">`.nuspec`: Označuje typ balíčku v rámci `packageTypes\packageType` pod uzlem `<metadata>` element:</span><span class="sxs-lookup"><span data-stu-id="462a0-114">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
