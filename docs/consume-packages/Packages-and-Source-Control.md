---
title: Balíčky NuGet a směřované zdroje
description: Důležité informace o tom, jak zacházet s balíčky NuGet v rámci správy verzí a systémů správy zdrojového kódu a jak vynechat balíčky s git a TFVC.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9d9ea10ccd32bb65ad0d62b591f5e2cb58ea3427
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "69019983"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="2ccd6-103">Vynechání balíčků NuGet v systémech správy zdrojového kódu</span><span class="sxs-lookup"><span data-stu-id="2ccd6-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="2ccd6-104">Vývojáři obvykle vynechat Balíčky NuGet z jejich úložiště správy zdrojového kódu a místo toho spoléhat na [obnovení balíčku](package-restore.md) přeinstalovat závislosti projektu před sestavením.</span><span class="sxs-lookup"><span data-stu-id="2ccd6-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="2ccd6-105">Důvody pro spoléhání se na obnovení balíčku patří následující:</span><span class="sxs-lookup"><span data-stu-id="2ccd6-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="2ccd6-106">Distribuované systémy správy verzí, jako je Git, obsahují úplné kopie všech verzí každého souboru v úložišti.</span><span class="sxs-lookup"><span data-stu-id="2ccd6-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="2ccd6-107">Binární soubory, které jsou často aktualizovány vést k významné nafouknutí a prodlužuje čas potřebný ke klonování úložiště.</span><span class="sxs-lookup"><span data-stu-id="2ccd6-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="2ccd6-108">Pokud jsou balíčky zahrnuty v úložišti, vývojáři mohou přidat odkazy přímo na obsah balíčku na disku, nikoli odkazování na balíčky prostřednictvím NuGet, což může vést k pevně zakódované názvy cest v projektu.</span><span class="sxs-lookup"><span data-stu-id="2ccd6-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="2ccd6-109">Je stále těžší vyčistit vaše řešení všech nepoužívaných složek balíčků, protože je třeba zajistit, že neodstraníte žádné složky balíčků, které jsou stále používány.</span><span class="sxs-lookup"><span data-stu-id="2ccd6-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="2ccd6-110">Vynecháním balíčků udržujete čisté hranice vlastnictví mezi kódem a balíčky od ostatních, na kterých jste závislí.</span><span class="sxs-lookup"><span data-stu-id="2ccd6-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="2ccd6-111">Mnoho balíčků NuGet jsou udržovány ve svých vlastních úložištích správy zdrojového kódu již.</span><span class="sxs-lookup"><span data-stu-id="2ccd6-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="2ccd6-112">Přestože obnovení balíčku je výchozí chování s NuGet, některé&mdash;ruční práce `packages` je nutné&mdash;vynechat balíčky konkrétně složku v projektu ze správy zdrojového kódu, jak je popsáno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="2ccd6-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="2ccd6-113">Vynechání balíčků s Gitem</span><span class="sxs-lookup"><span data-stu-id="2ccd6-113">Omitting packages with Git</span></span>

<span data-ttu-id="2ccd6-114">Pomocí [souboru .gitignore](https://git-scm.com/docs/gitignore) můžete mimo`.nupkg`jiné `packages` ignorovat `project.assets.json`balíčky NuGet ( ) a , mimo jiné.</span><span class="sxs-lookup"><span data-stu-id="2ccd6-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="2ccd6-115">Další informace naleznete v [ukázce `.gitignore` pro projekty sady Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span><span class="sxs-lookup"><span data-stu-id="2ccd6-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="2ccd6-116">Důležité části souboru `.gitignore` jsou:</span><span class="sxs-lookup"><span data-stu-id="2ccd6-116">The important parts of the `.gitignore` file are:</span></span>

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

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="2ccd6-117">Vynechání balíčků se spouštěním verzí Team Foundation</span><span class="sxs-lookup"><span data-stu-id="2ccd6-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="2ccd6-118">Před *přidáním* projektu do správy zdrojového kódu postupujte podle těchto pokynů, pokud je to možné.</span><span class="sxs-lookup"><span data-stu-id="2ccd6-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="2ccd6-119">V opačném případě `packages` ručně odstraňte složku z úložiště a před pokračováním tuto změnu sezměna odevzdejte se změnami.</span><span class="sxs-lookup"><span data-stu-id="2ccd6-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="2ccd6-120">Zakázání integrace správy zdrojového kódu s TFVC pro vybrané soubory:</span><span class="sxs-lookup"><span data-stu-id="2ccd6-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="2ccd6-121">Vytvořte složku `.nuget` volanou ve `.sln` složce řešení (kde je soubor).</span><span class="sxs-lookup"><span data-stu-id="2ccd6-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="2ccd6-122">Tip: V systému Windows, chcete-li vytvořit `.nuget.` tuto složku v Průzkumníkovi Windows, použijte název *s* koncovou tečkou.</span><span class="sxs-lookup"><span data-stu-id="2ccd6-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="2ccd6-123">V této složce vytvořte soubor s názvem `NuGet.Config` a otevřete jej pro úpravy.</span><span class="sxs-lookup"><span data-stu-id="2ccd6-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="2ccd6-124">Přidejte jako minimum následující text, kde nastavení [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) instruuje Visual Studio přeskočit vše ve `packages` složce:</span><span class="sxs-lookup"><span data-stu-id="2ccd6-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="2ccd6-125">Pokud používáte TFS 2010 nebo `packages` starší, maskovat složku v mapování pracovního prostoru.</span><span class="sxs-lookup"><span data-stu-id="2ccd6-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="2ccd6-126">Na TFS 2012 nebo novější nebo pomocí Visual `.tfignore` Studio Team Services vytvořte soubor, jak je popsáno v části [Přidat soubory na server](/vsts/tfvc/add-files-server?view=vsts#tfignore).</span><span class="sxs-lookup"><span data-stu-id="2ccd6-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [Add Files to the Server](/vsts/tfvc/add-files-server?view=vsts#tfignore).</span></span> <span data-ttu-id="2ccd6-127">Do tohoto souboru zahrňte níže uvedený `\packages` obsah, abyste explicitně ignorovali změny složky na úrovni úložiště a několik dalších zprostředkujících souborů.</span><span class="sxs-lookup"><span data-stu-id="2ccd6-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="2ccd6-128">(Soubor můžete vytvořit v Průzkumníkovi Windows `.tfignore.` pomocí názvu a s koncovou tečkou, ale možná budete muset nejprve zakázat možnost Skrýt známé přípony souborů.):</span><span class="sxs-lookup"><span data-stu-id="2ccd6-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="2ccd6-129">`NuGet.Config` Přidejte `.tfignore` a do správy zdrojového kódu a vrácení změn se změnami.</span><span class="sxs-lookup"><span data-stu-id="2ccd6-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
