---
title: Balíčky NuGet a Správa zdrojového kódu
description: Informace o tom, jak zacházet s balíčky NuGet v rámci správy verzí a systémy správy zdrojového kódu a jak vynechat balíčky pomocí Gitu a TFVC.
author: JonDouglas
ms.author: jodou
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9bae65573ca49c68d07250228c1923890e0f14ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775017"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="012ea-103">Vynechávání balíčků NuGet v systémech správy zdrojového kódu</span><span class="sxs-lookup"><span data-stu-id="012ea-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="012ea-104">Vývojáři obvykle vynechává balíčky NuGet ze svých úložišť správy zdrojového kódu a využívají se místo toho, aby [obnovily](package-restore.md) závislosti projektu před sestavením.</span><span class="sxs-lookup"><span data-stu-id="012ea-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="012ea-105">Důvody pro spoléhání na obnovení balíčku zahrnují následující:</span><span class="sxs-lookup"><span data-stu-id="012ea-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="012ea-106">Distribuované systémy správy verzí, jako je git, obsahují úplné kopie každé verze každého souboru v úložišti.</span><span class="sxs-lookup"><span data-stu-id="012ea-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="012ea-107">Binární soubory, které se často aktualizují, vedou k významným dispozici determinističtějšíům a prodlouží dobu potřebnou k naklonování úložiště.</span><span class="sxs-lookup"><span data-stu-id="012ea-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="012ea-108">Když jsou balíčky zahrnuté do úložiště, můžou vývojáři přidat odkazy přímo na obsah balíčku na disku místo na odkazování na balíčky přes NuGet, což může vést k pevně zakódovaným názvům cest v projektu.</span><span class="sxs-lookup"><span data-stu-id="012ea-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="012ea-109">Je obtížnější vyčistit řešení všech nepoužívaných složek balíčku, protože je potřeba zajistit, aby se neodstranily žádné složky balíčku, které se pořád používají.</span><span class="sxs-lookup"><span data-stu-id="012ea-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="012ea-110">Vynecháním balíčků zachováte čisté hranice vlastnictví mezi kódem a balíčky od ostatních, na kterých jste závislí.</span><span class="sxs-lookup"><span data-stu-id="012ea-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="012ea-111">Mnoho balíčků NuGet se už ve vlastních úložištích správy zdrojových kódů udržuje.</span><span class="sxs-lookup"><span data-stu-id="012ea-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="012ea-112">I když je obnovení balíčku výchozím chováním nástroje NuGet, některé ruční práce jsou nezbytné k vynechání balíčků &mdash; konkrétně, `packages` ze složky v projektu &mdash; ze správy zdrojového kódu, jak je popsáno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="012ea-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="012ea-113">Vynechávání balíčků v Gitu</span><span class="sxs-lookup"><span data-stu-id="012ea-113">Omitting packages with Git</span></span>

<span data-ttu-id="012ea-114">Pomocí [souboru. gitignore](https://git-scm.com/docs/gitignore) můžete ignorovat balíčky NuGet ( `.nupkg` ) `packages` složku, a `project.assets.json` mimo jiné.</span><span class="sxs-lookup"><span data-stu-id="012ea-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="012ea-115">Referenční informace naleznete v [ukázce `.gitignore` pro projekty sady Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span><span class="sxs-lookup"><span data-stu-id="012ea-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="012ea-116">Důležité části `.gitignore` souboru jsou:</span><span class="sxs-lookup"><span data-stu-id="012ea-116">The important parts of the `.gitignore` file are:</span></span>

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

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="012ea-117">Vynechávání balíčků s Správa verzí Team Foundation</span><span class="sxs-lookup"><span data-stu-id="012ea-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="012ea-118">Pokud je to možné, postupujte podle těchto pokynů, *než* přidáte projekt do správy zdrojových kódů.</span><span class="sxs-lookup"><span data-stu-id="012ea-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="012ea-119">V opačném případě ručně odstraňte `packages` složku z úložiště a vraťte se změnami, než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="012ea-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="012ea-120">Chcete-li zakázat integraci správy zdrojového kódu s TFVC pro vybrané soubory:</span><span class="sxs-lookup"><span data-stu-id="012ea-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="012ea-121">Ve složce řešení vytvořte složku s názvem `.nuget` (kde `.sln` je soubor).</span><span class="sxs-lookup"><span data-stu-id="012ea-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="012ea-122">Tip: v systému Windows Chcete-li vytvořit tuto složku v Průzkumníku Windows, použijte název `.nuget.` *s* koncovou tečkou.</span><span class="sxs-lookup"><span data-stu-id="012ea-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="012ea-123">V této složce vytvořte soubor s názvem `NuGet.Config` a otevřete ho pro úpravy.</span><span class="sxs-lookup"><span data-stu-id="012ea-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="012ea-124">Přidejte následující text jako minimální, kde nastavení [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) vydá aplikaci Visual Studio, aby přeskočila vše ve `packages` složce:</span><span class="sxs-lookup"><span data-stu-id="012ea-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="012ea-125">Pokud používáte TFS 2010 nebo starší, skryté `packages` složky v mapování pracovních prostorů.</span><span class="sxs-lookup"><span data-stu-id="012ea-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="012ea-126">Na serveru TFS 2012 nebo novějším nebo pomocí Visual Studio Team Services vytvořte `.tfignore` soubor, jak je popsáno v tématu [Přidání souborů na server](/vsts/tfvc/add-files-server?view=vsts#tfignore).</span><span class="sxs-lookup"><span data-stu-id="012ea-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [Add Files to the Server](/vsts/tfvc/add-files-server?view=vsts#tfignore).</span></span> <span data-ttu-id="012ea-127">V tomto souboru zahrňte níže uvedený obsah, který explicitně ignoruje změny `\packages` složky na úrovni úložiště a několik dalších zprostředkujících souborů.</span><span class="sxs-lookup"><span data-stu-id="012ea-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="012ea-128">(Soubor můžete vytvořit v Průzkumníkovi Windows pomocí názvu a `.tfignore.` s koncovou tečkou, ale možná budete muset nejdřív zakázat možnost "Skrýt známé přípony souborů".):</span><span class="sxs-lookup"><span data-stu-id="012ea-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

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

1. <span data-ttu-id="012ea-129">Přidejte `NuGet.Config` a `.tfignore` do správy zdrojových kódů a vraťte se změnami.</span><span class="sxs-lookup"><span data-stu-id="012ea-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
