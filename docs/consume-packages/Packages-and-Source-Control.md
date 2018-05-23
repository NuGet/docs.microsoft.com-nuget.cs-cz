---
title: Balíčky NuGet a Správa zdrojového kódu
description: Důležité informace týkající se má stát s balíčků NuGet v rámci správy verzí a zdroj řízení systémů a jak vynechejte balíčky s git a TFVC.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: bc2c6d5e9933f2f6103363a2e69fbb9b47f80ecf
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/22/2018
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="f617e-103">Vynechání balíčky NuGet ve zdrojových systémech ovládací prvek</span><span class="sxs-lookup"><span data-stu-id="f617e-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="f617e-104">Vývojáři obvykle vynechejte balíčky NuGet z jejich zdrojová ovládací prvek úložiště a místo toho spoléhají na [obnovení balíčků](package-restore.md) přeinstalovat projektu závislosti před sestavení.</span><span class="sxs-lookup"><span data-stu-id="f617e-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="f617e-105">Důvody pro spoléhat na obnovení balíčků zahrnují následující:</span><span class="sxs-lookup"><span data-stu-id="f617e-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="f617e-106">Distribuované verze řízení systémů, jako je například Git, zahrnují úplnou kopií každé verzi každého souboru v úložišti.</span><span class="sxs-lookup"><span data-stu-id="f617e-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="f617e-107">Binární soubory, které jsou často aktualizované vést k výrazné tomu a prodlouží dobu potřebnou k klonovat úložiště.</span><span class="sxs-lookup"><span data-stu-id="f617e-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="f617e-108">Když balíčky jsou zahrnuty v úložišti, podléhají vývojáři přidáte odkazy na obsah balíčku přímo na disku než odkazující balíčky prostřednictvím balíčku NuGet, což může vést k názvy pevně cest v projektu.</span><span class="sxs-lookup"><span data-stu-id="f617e-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="f617e-109">Bude těžší Vyčistit řešení nepoužívá balíček složek, jako je třeba zajistit, že nemáte odstranit všechny složky balíčku stále používáno.</span><span class="sxs-lookup"><span data-stu-id="f617e-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="f617e-110">Díky vynechání balíčky, Udržovat čistou hranice vlastnictví až balíčky od ostatních, které závisí na kódu.</span><span class="sxs-lookup"><span data-stu-id="f617e-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="f617e-111">Mnoho balíčky NuGet jsou zachována ve své vlastní zdrojová úložiště ovládací prvek již.</span><span class="sxs-lookup"><span data-stu-id="f617e-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="f617e-112">I když se obnovení balíčku je výchozí chování u balíčku NuGet, některé ručního nastavení je potřeba vynechejte balíčky&mdash;konkrétně, `packages` složku ve vašem projektu&mdash;od správy zdrojového kódu, jak je popsáno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="f617e-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="f617e-113">Vynechání balíčky s Gitem</span><span class="sxs-lookup"><span data-stu-id="f617e-113">Omitting packages with Git</span></span>

<span data-ttu-id="f617e-114">Použití [soubor .gitignore](https://git-scm.com/docs/gitignore) ignorovat balíčky NuGet (`.nupkg`) `packages` složku, a `project.assets.json`, mimo jiné.</span><span class="sxs-lookup"><span data-stu-id="f617e-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="f617e-115">Odkaz, najdete v článku [ukázka `.gitignore` pro projekty v sadě Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span><span class="sxs-lookup"><span data-stu-id="f617e-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="f617e-116">Důležitou součástí `.gitignore` souboru jsou:</span><span class="sxs-lookup"><span data-stu-id="f617e-116">The important parts of the `.gitignore` file are:</span></span>

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="f617e-117">Vynechání balíčky s verzí Team Foundation</span><span class="sxs-lookup"><span data-stu-id="f617e-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="f617e-118">Pokud je to možné postupovat podle těchto pokynů *před* přidání projektu do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="f617e-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="f617e-119">Jinak, odstraňte ručně `packages` složky z úložiště a tato změna před pokračováním se změnami.</span><span class="sxs-lookup"><span data-stu-id="f617e-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="f617e-120">Postup při zakázání integrace ovládacích prvků zdrojového s TFVC pro vybrané soubory:</span><span class="sxs-lookup"><span data-stu-id="f617e-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="f617e-121">Vytvořte složku s názvem `.nuget` ve složce řešení (kde `.sln` soubor).</span><span class="sxs-lookup"><span data-stu-id="f617e-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="f617e-122">Tip: v systému Windows, k vytvoření této složky v Průzkumníku Windows, použijte název `.nuget.` *s* koncovou tečku.</span><span class="sxs-lookup"><span data-stu-id="f617e-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="f617e-123">V této složce vytvořte soubor s názvem `NuGet.Config` a otevřete pro úpravy.</span><span class="sxs-lookup"><span data-stu-id="f617e-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="f617e-124">Přidejte následující text jako minimální, kde [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) nastavení dá pokyn chcete přeskočit všechno ve Visual Studio `packages` složky:</span><span class="sxs-lookup"><span data-stu-id="f617e-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="f617e-125">Pokud používáte sady TFS 2010 nebo starší, cloak `packages` složky mapování pracovního prostoru.</span><span class="sxs-lookup"><span data-stu-id="f617e-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="f617e-126">V sadě TFS 2012 nebo novější, nebo s Visual Studio Team Services, vytvořit `.tfignore` souboru, jak je popsáno na [AddFiles k serveru](/vsts/tfvc/add-files-server.md?view=vsts#tfignore).</span><span class="sxs-lookup"><span data-stu-id="f617e-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [AddFiles to the Server](/vsts/tfvc/add-files-server.md?view=vsts#tfignore).</span></span> <span data-ttu-id="f617e-127">V tomto souboru zahrnout obsah níže explicitně Ignorovat změny `\packages` složky na úrovni úložiště a několik dalších zprostředkující soubory.</span><span class="sxs-lookup"><span data-stu-id="f617e-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="f617e-128">(Soubor můžete vytvořit v Průzkumníku Windows pomocí názvu `.tfignore.` s koncovou tečku, ale může být nutné zakázat "Skrýt známému souboru rozšíření" možnost nejprve.):</span><span class="sxs-lookup"><span data-stu-id="f617e-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Exclude package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="f617e-129">Přidat `NuGet.Config` a `.tfignore` ovládací prvek zdroje a změny se změnami.</span><span class="sxs-lookup"><span data-stu-id="f617e-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
