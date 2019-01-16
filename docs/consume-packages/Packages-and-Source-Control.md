---
title: Balíčky NuGet a Správa zdrojového kódu
description: Důležité informace o tom, jak nakládat s balíčky NuGet v rámci systémy správy verzí ovládacího prvku a zdroje a jak chcete vynechat, nechte balíčky s git a TFVC.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: ef4c45451cc52eb08dc627f8442c48e853d8ceaf
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324731"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="23441-103">Vynechání balíčky NuGet v systémy správy zdrojového kódu</span><span class="sxs-lookup"><span data-stu-id="23441-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="23441-104">Vývojáři obvykle vynechat balíčků NuGet z jejich úložiště správy zdrojového kódu a místo toho spoléhají na [obnovení balíčků](package-restore.md) přeinstalovat závislosti projektu před během sestavení.</span><span class="sxs-lookup"><span data-stu-id="23441-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="23441-105">Důvody pro spoléhání se na obnovení balíčků, patří:</span><span class="sxs-lookup"><span data-stu-id="23441-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="23441-106">Systémy správy distribuovaných verzí, jako je Git, zahrnout úplné kopie každé verze každého souboru v rámci tohoto úložiště.</span><span class="sxs-lookup"><span data-stu-id="23441-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="23441-107">Binární soubory, které se často aktualizují vést k výrazné determinističtější a prodlouží čas potřebný ke klonování úložiště.</span><span class="sxs-lookup"><span data-stu-id="23441-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="23441-108">Při balíčky jsou zahrnuty v úložišti, mohou vývojáři přidat odkazy přímo na obsah balíčku na disku než odkazující balíčků prostřednictvím balíčku NuGet, což může vést k názvům pevně zakódované cesty v projektu.</span><span class="sxs-lookup"><span data-stu-id="23441-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="23441-109">Bude obtížnější Vyčistit řešení složek nepoužívaných balíčků, jako je nutné se ujistit, že nechcete odstranit všechny složky balíčku stále používán.</span><span class="sxs-lookup"><span data-stu-id="23441-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="23441-110">Vynecháním balíčky udržovat čisté hranice vlastnictví mezi kódu a balíčků od ostatních, které závisí na aplikaci.</span><span class="sxs-lookup"><span data-stu-id="23441-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="23441-111">Mnoho balíčky NuGet jsou zachována ve své vlastní úložiště správy zdrojového kódu už.</span><span class="sxs-lookup"><span data-stu-id="23441-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="23441-112">Výchozí chování nuget sice obnovit balíček úkony ruční je nezbytné vynechejte balíčky&mdash;totiž, `packages` složku ve vašem projektu&mdash;ze správy zdrojového kódu, jak je popsáno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="23441-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="23441-113">Vynechání balíčky s Gitem</span><span class="sxs-lookup"><span data-stu-id="23441-113">Omitting packages with Git</span></span>

<span data-ttu-id="23441-114">Použití [soubor .gitignore](https://git-scm.com/docs/gitignore) ignorovat balíčky NuGet (`.nupkg`) `packages` složky, a `project.assets.json`, mimo jiné.</span><span class="sxs-lookup"><span data-stu-id="23441-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="23441-115">Odkaz, najdete v článku [ukázka `.gitignore` pro projekty aplikace Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span><span class="sxs-lookup"><span data-stu-id="23441-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="23441-116">Důležité části `.gitignore` souboru jsou:</span><span class="sxs-lookup"><span data-stu-id="23441-116">The important parts of the `.gitignore` file are:</span></span>

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

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="23441-117">Vynechání balíčky s Team Foundation – správa verzí</span><span class="sxs-lookup"><span data-stu-id="23441-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="23441-118">Pokud je to možné postupujte podle těchto pokynů *před* přidání projektu do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="23441-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="23441-119">V opačném případě odstraňte ručně `packages` složku z vašeho úložiště a vrácení se změnami tuto změnu, než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="23441-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="23441-120">Chcete-li zakázat integrace správy zdrojového kódu s TFVC pro vybrané soubory:</span><span class="sxs-lookup"><span data-stu-id="23441-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="23441-121">Vytvořte složku s názvem `.nuget` ve složce řešení (kde `.sln` soubor).</span><span class="sxs-lookup"><span data-stu-id="23441-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="23441-122">Tip: na Windows, k vytvoření této složky v Průzkumníku Windows, použijte název `.nuget.` *s* koncovou tečku.</span><span class="sxs-lookup"><span data-stu-id="23441-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="23441-123">V této složce vytvořte soubor s názvem `NuGet.Config` a otevřete pro úpravy.</span><span class="sxs-lookup"><span data-stu-id="23441-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="23441-124">Přidejte následující text jako minimum, kde [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) nastavení dá pokyn Přeskočit vše v sadě Visual Studio `packages` složky:</span><span class="sxs-lookup"><span data-stu-id="23441-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="23441-125">Pokud používáte TFS 2010 nebo starší, skrytí `packages` složky v mapování pracovního prostoru.</span><span class="sxs-lookup"><span data-stu-id="23441-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="23441-126">Na serveru TFS 2012 nebo novější, nebo službou Visual Studio Team Services, vytvořit `.tfignore` sdílené, jak je popsáno na [přidat soubory serveru](/vsts/tfvc/add-files-server?view=vsts#tfignore).</span><span class="sxs-lookup"><span data-stu-id="23441-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [Add Files to the Server](/vsts/tfvc/add-files-server?view=vsts#tfignore).</span></span> <span data-ttu-id="23441-127">V tomto souboru zahrnují následující explicitně Ignorovat změny obsah `\packages` složky na úrovni úložiště a několik dalších zprostředkujících souborů.</span><span class="sxs-lookup"><span data-stu-id="23441-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="23441-128">(Tento soubor můžete vytvořit v Průzkumníku Windows pomocí názvu `.tfignore.` s koncovou tečku, ale může být nutné zakázat "Skrýt příponu souborů známých" možnost nejprve.):</span><span class="sxs-lookup"><span data-stu-id="23441-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

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

1. <span data-ttu-id="23441-129">Přidat `NuGet.Config` a `.tfignore` do správy zdrojového kódu a vrácení zpět se změnami.</span><span class="sxs-lookup"><span data-stu-id="23441-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
