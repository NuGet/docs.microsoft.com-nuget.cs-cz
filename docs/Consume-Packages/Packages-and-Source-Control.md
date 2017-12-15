---
title: "Balíčky NuGet a Správa zdrojového kódu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c874e6f-99eb-46dd-997f-f67d98d0237e
description: "Důležité informace týkající se má stát s balíčků NuGet v rámci správy verzí a zdroj řízení systémů a jak vynechejte balíčky s git a TFVC."
keywords: "Řízení úložiště NuGet zdrojového kódu, NuGet verzí, NuGet a git, NuGet a sady TFS, NuGet a TFVC, vynechejte balíčky, zdrojová ovládací prvek úložiště, verze"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c73dea74f2363f49fb476a5812c29de63fec89a3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="6e813-104">Vynechání balíčky NuGet ve zdrojových systémech ovládací prvek</span><span class="sxs-lookup"><span data-stu-id="6e813-104">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="6e813-105">Vývojáři obvykle vynechejte balíčky NuGet z jejich zdrojová ovládací prvek úložiště a místo toho spoléhají na [obnovení balíčků](../consume-packages/package-restore.md) přeinstalovat projektu závislosti před sestavení.</span><span class="sxs-lookup"><span data-stu-id="6e813-105">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](../consume-packages/package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="6e813-106">Důvody pro spoléhat na obnovení balíčků zahrnují následující:</span><span class="sxs-lookup"><span data-stu-id="6e813-106">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="6e813-107">Distribuované verze řízení systémů, jako je například Git, zahrnují úplnou kopií každé verzi každého souboru v úložišti.</span><span class="sxs-lookup"><span data-stu-id="6e813-107">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="6e813-108">Binární soubory, které jsou často aktualizované vést k výrazné tomu a prodlouží dobu potřebnou k klonovat úložiště.</span><span class="sxs-lookup"><span data-stu-id="6e813-108">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="6e813-109">Když balíčky jsou zahrnuty v úložišti, podléhají vývojáři přidáte odkazy na obsah balíčku přímo na disku než odkazující balíčky prostřednictvím balíčku NuGet, což může vést k názvy pevně cest v projektu.</span><span class="sxs-lookup"><span data-stu-id="6e813-109">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="6e813-110">Bude těžší Vyčistit řešení nepoužívá balíček složek, jako je třeba zajistit, že nemáte odstranit všechny složky balíčku stále používáno.</span><span class="sxs-lookup"><span data-stu-id="6e813-110">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="6e813-111">Díky vynechání balíčky, Udržovat čistou hranice vlastnictví až balíčky od ostatních, které závisí na kódu.</span><span class="sxs-lookup"><span data-stu-id="6e813-111">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="6e813-112">Mnoho balíčky NuGet jsou zachována ve své vlastní zdrojová úložiště ovládací prvek již.</span><span class="sxs-lookup"><span data-stu-id="6e813-112">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="6e813-113">I když se obnovení balíčku je výchozí chování u balíčku NuGet, některé ručního nastavení je potřeba vynechejte balíčky&mdash;konkrétně, `packages` složku ve vašem projektu&mdash;od správy zdrojového kódu, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="6e813-113">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in the following sections.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="6e813-114">Vynechání balíčky s Gitem</span><span class="sxs-lookup"><span data-stu-id="6e813-114">Omitting packages with Git</span></span>

<span data-ttu-id="6e813-115">Použití [soubor .gitignore](https://git-scm.com/docs/gitignore) předejdete včetně `packages` složky ve správě zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="6e813-115">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to avoid including the `packages` folder in source control.</span></span> <span data-ttu-id="6e813-116">Odkaz, najdete v článku [ukázka `.gitignore` pro projekty v sadě Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="6e813-116">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="6e813-117">Důležitou součástí `.gitignore` souboru jsou:</span><span class="sxs-lookup"><span data-stu-id="6e813-117">The important parts of the `.gitignore` file are:</span></span>

```
# Ignore NuGet Packages
*.nupkg

# Ignore the packages folder
**/packages/*

# Include packages/build/, which is used as an MSBuild target
!**/packages/build/

# Uncomment if necessary; generally it's regenerated when needed
#!**/packages/repositories.config

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json; project.assets.json is used in conjunction with the PackageReference format.
project.lock.json
project.assets.json
*.nuget.props
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="6e813-118">Vynechání balíčky s verzí Team Foundation</span><span class="sxs-lookup"><span data-stu-id="6e813-118">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="6e813-119">Pokud je to možné postupovat podle těchto pokynů *před* přidání projektu do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="6e813-119">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="6e813-120">Jinak, odstraňte ručně `packages` složky z úložiště a tato změna před pokračováním se změnami.</span><span class="sxs-lookup"><span data-stu-id="6e813-120">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="6e813-121">Postup při zakázání integrace ovládacích prvků zdrojového s TFVC pro vybrané soubory:</span><span class="sxs-lookup"><span data-stu-id="6e813-121">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="6e813-122">Vytvořte složku s názvem `.nuget` ve složce řešení (kde `.sln` soubor).</span><span class="sxs-lookup"><span data-stu-id="6e813-122">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="6e813-123">Tip: v systému Windows, k vytvoření této složky v Průzkumníku Windows, použijte název `.nuget.` *s* koncovou tečku.</span><span class="sxs-lookup"><span data-stu-id="6e813-123">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="6e813-124">V této složce vytvořte soubor s názvem `NuGet.Config` a otevřete pro úpravy.</span><span class="sxs-lookup"><span data-stu-id="6e813-124">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="6e813-125">Přidejte následující text jako minimální, kde [disableSourceControlIntegration](../Schema/nuget-config-file.md#solution-section) nastavení dá pokyn chcete přeskočit všechno ve Visual Studio `packages` složky:</span><span class="sxs-lookup"><span data-stu-id="6e813-125">Add the following text as a minimum, where the [disableSourceControlIntegration](../Schema/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="6e813-126">Pokud používáte sady TFS 2010 nebo starší, cloak `packages` složky mapování pracovního prostoru.</span><span class="sxs-lookup"><span data-stu-id="6e813-126">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="6e813-127">V sadě TFS 2012 nebo novější, nebo s Visual Studio Team Services, vytvořit `.tfignore` souboru, jak je popsáno na [AddFiles k serveru](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore).</span><span class="sxs-lookup"><span data-stu-id="6e813-127">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [AddFiles to the Server](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore).</span></span> <span data-ttu-id="6e813-128">V tomto souboru zahrnout obsah níže explicitně Ignorovat změny `\packages` složky na úrovni úložiště a několik dalších zprostředkující soubory.</span><span class="sxs-lookup"><span data-stu-id="6e813-128">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="6e813-129">(Soubor můžete vytvořit v Průzkumníku Windows pomocí názvu `.tfignore.` s koncovou tečku, ale může být nutné zakázat "Skrýt známému souboru rozšíření" možnost nejprve.):</span><span class="sxs-lookup"><span data-stu-id="6e813-129">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```
   # Ignore NuGet Packages
   *.nupkg   

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Include package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="6e813-130">Přidat `NuGet.Config` a `.tfignore` ovládací prvek zdroje a změny se změnami.</span><span class="sxs-lookup"><span data-stu-id="6e813-130">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
