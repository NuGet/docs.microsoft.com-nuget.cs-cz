---
title: Nastavení místních informačních kanálů NuGet
description: Postup vytvoření místního kanálu pro balíčky NuGet pomocí složek v místní síti
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 42a5c30c058a9efb35338c1b484235b6ad111bd0
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317595"
---
# <a name="local-feeds"></a><span data-ttu-id="ea4c3-103">Místní informační kanály</span><span class="sxs-lookup"><span data-stu-id="ea4c3-103">Local feeds</span></span>

<span data-ttu-id="ea4c3-104">Místní kanály balíčků NuGet jsou jednoduše hierarchické struktury složek v místní síti (nebo dokonce jenom v počítači), do kterých umístíte balíčky.</span><span class="sxs-lookup"><span data-stu-id="ea4c3-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="ea4c3-105">Tyto kanály se pak dají použít jako zdroje balíčků se všemi ostatními operacemi NuGet pomocí rozhraní příkazového řádku, uživatelského rozhraní Správce balíčků a konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="ea4c3-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="ea4c3-106">Pokud chcete zdroj povolit, přidejte jeho cestu (například `\\myserver\packages`) do seznamu zdrojů pomocí [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) uživatelského rozhraní [Správce balíčků](../consume-packages/install-use-packages-visual-studio.md#package-sources) nebo příkazu.</span><span class="sxs-lookup"><span data-stu-id="ea4c3-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md#package-sources) or the [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="ea4c3-107">Hierarchické struktury složek jsou podporovány v NuGet 3.3 +.</span><span class="sxs-lookup"><span data-stu-id="ea4c3-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="ea4c3-108">Starší verze NuGet používají jenom jednu složku obsahující balíčky, jejichž výkon je mnohem menší než hierarchická struktura.</span><span class="sxs-lookup"><span data-stu-id="ea4c3-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="ea4c3-109">Inicializace a údržba hierarchických složek</span><span class="sxs-lookup"><span data-stu-id="ea4c3-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="ea4c3-110">Stromová struktura složky hierarchické verze má následující obecnou strukturu:</span><span class="sxs-lookup"><span data-stu-id="ea4c3-110">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="ea4c3-111">NuGet tuto strukturu vytvoří automaticky, když použijete [`nuget add`](../reference/cli-reference/cli-ref-add.md) příkaz ke zkopírování balíčku do informačního kanálu:</span><span class="sxs-lookup"><span data-stu-id="ea4c3-111">NuGet creates this structure automatically when you use the [`nuget add`](../reference/cli-reference/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="ea4c3-112">`nuget add` Příkaz funguje současně s jedním balíčkem, což může být nepraktické při vytváření informačního kanálu s více balíčky.</span><span class="sxs-lookup"><span data-stu-id="ea4c3-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="ea4c3-113">V takových případech použijte [`nuget init`](../reference/cli-reference/cli-ref-init.md) příkaz ke zkopírování všech balíčků do složky do informačního kanálu, jako kdyby byl každý z nich spuštěn `nuget add` samostatně.</span><span class="sxs-lookup"><span data-stu-id="ea4c3-113">In such cases, use the [`nuget init`](../reference/cli-reference/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="ea4c3-114">Například následující příkaz zkopíruje všechny balíčky z `c:\packages` do hierarchické stromové struktury na: `\\myserver\packages`</span><span class="sxs-lookup"><span data-stu-id="ea4c3-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="ea4c3-115">Stejně jako u `add` `init` příkazu vytvoří složku pro každý identifikátor balíčku, který obsahuje složku s číslem verze, v rámci které je příslušný balíček.</span><span class="sxs-lookup"><span data-stu-id="ea4c3-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
