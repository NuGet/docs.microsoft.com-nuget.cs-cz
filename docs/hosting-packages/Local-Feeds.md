---
title: Nastavení místní informační kanály NuGet
description: Jak vytvořit místní informační kanál pro balíčky NuGet pomocí složky ve vaší místní síti
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 91c072c8895ab4267c64fd04deae010ae5af4d37
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545449"
---
# <a name="local-feeds"></a><span data-ttu-id="5fd6e-103">Místní informační kanály</span><span class="sxs-lookup"><span data-stu-id="5fd6e-103">Local feeds</span></span>

<span data-ttu-id="5fd6e-104">Místní informační kanály balíčků NuGet se jednoduše hierarchickým struktur ve vaší místní síti (nebo jenom svého počítače) ve které umístíte balíčky.</span><span class="sxs-lookup"><span data-stu-id="5fd6e-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="5fd6e-105">Tyto kanály můžete pak použít jako zdroje balíčků se všechny ostatní operace NuGet pomocí rozhraní příkazového řádku, uživatelské rozhraní Správce balíčků a konzole Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="5fd6e-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="5fd6e-106">Povolit zdroji, přidejte jeho cesta (například `\\myserver\packages`) do seznamu zdrojů pomocí [uživatelské rozhraní Správce balíčků](../tools/package-manager-ui.md#package-sources) nebo [ `nuget sources` ](../tools/cli-ref-sources.md) příkaz.</span><span class="sxs-lookup"><span data-stu-id="5fd6e-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../tools/package-manager-ui.md#package-sources) or the [`nuget sources`](../tools/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="5fd6e-107">Hierarchickým struktury jsou podporovány ve Správci NuGet 3.3 +.</span><span class="sxs-lookup"><span data-stu-id="5fd6e-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="5fd6e-108">Starší verze balíčku NuGet používat jenom jednu složku obsahující balíčky, s nimiž je mnohem nižší než hierarchickou strukturu výkonu.</span><span class="sxs-lookup"><span data-stu-id="5fd6e-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="5fd6e-109">Inicializace a udržování hierarchické složky</span><span class="sxs-lookup"><span data-stu-id="5fd6e-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="5fd6e-110">Strom hierarchických označené verzí složek má následující obecnou strukturu:</span><span class="sxs-lookup"><span data-stu-id="5fd6e-110">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="5fd6e-111">NuGet tato struktura automaticky vytvoří při použití [ `nuget add` ](../tools/cli-ref-add.md) příkazu zkopírovat balíček do informačního kanálu:</span><span class="sxs-lookup"><span data-stu-id="5fd6e-111">NuGet creates this structure automatically when you use the [`nuget add`](../tools/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="5fd6e-112">`nuget add` Příkaz funguje s jeden balíček současně, což může být nepraktické při nastavování informační kanál s více balíčky.</span><span class="sxs-lookup"><span data-stu-id="5fd6e-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="5fd6e-113">V takovém případě použijte [ `nuget init` ](../tools/cli-ref-init.md) příkazu pro kopírování všech balíčků ve složce do informačního kanálu, jako kdyby jste spustili `nuget add` na každé z nich samostatně.</span><span class="sxs-lookup"><span data-stu-id="5fd6e-113">In such cases, use the [`nuget init`](../tools/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="5fd6e-114">Například následující příkaz zkopíruje všechny balíčky z `c:\packages` hierarchické stromové struktury na `\\myserver\packages`:</span><span class="sxs-lookup"><span data-stu-id="5fd6e-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="5fd6e-115">Stejně jako u `add` příkazu `init` vytvoří složku pro každý balíček identifikátor, z nichž každý obsahuje složku číslo verze, ve kterém je příslušný balíček.</span><span class="sxs-lookup"><span data-stu-id="5fd6e-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
