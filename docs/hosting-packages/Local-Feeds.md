---
title: Nastavení místního kanály NuGet
description: Jak vytvořit místní kanálu pro balíčky NuGet ve vaší místní síti pomocí složek
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 5d86657bdf26452d027593b953168e28694acf82
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818682"
---
# <a name="local-feeds"></a><span data-ttu-id="3041e-103">Místní informační kanály</span><span class="sxs-lookup"><span data-stu-id="3041e-103">Local feeds</span></span>

<span data-ttu-id="3041e-104">Místní kanály balíček NuGet se jednoduše hierarchické složky struktury v místní síti (nebo i právě svého počítače) ve které umístíte balíčky.</span><span class="sxs-lookup"><span data-stu-id="3041e-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="3041e-105">Tyto kanály můžete potom použít jako zdroje balíčků s všechny operace NuGet pomocí rozhraní příkazového řádku, uživatelské rozhraní Správce balíčků a konzola Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="3041e-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="3041e-106">Povolit zdroj, přidejte její název cesty (například `\\myserver\packages`) do seznamu zdroje pomocí [uživatelského rozhraní Správce balíčků](../tools/package-manager-ui.md#package-sources) nebo [ `nuget sources` ](../tools/cli-ref-sources.md) příkaz.</span><span class="sxs-lookup"><span data-stu-id="3041e-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../tools/package-manager-ui.md#package-sources) or the [`nuget sources`](../tools/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="3041e-107">Struktury hierarchické složky jsou podporovány v NuGet 3.3 +.</span><span class="sxs-lookup"><span data-stu-id="3041e-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="3041e-108">Starší verze NuGet použijte pouze jednu složku obsahující balíčky, se kterými je mnohem nižší než hierarchická struktura výkonu.</span><span class="sxs-lookup"><span data-stu-id="3041e-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="3041e-109">Inicializace a údržbu hierarchické složek</span><span class="sxs-lookup"><span data-stu-id="3041e-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="3041e-110">Strom hierarchické verzí složek má následující obecné strukturu:</span><span class="sxs-lookup"><span data-stu-id="3041e-110">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="3041e-111">NuGet tato struktura automaticky vytvoří při použití [ `nuget add` ](../tools/cli-ref-add.md) příkazu zkopírovat balíček do informačního kanálu:</span><span class="sxs-lookup"><span data-stu-id="3041e-111">NuGet creates this structure automatically when you use the [`nuget add`](../tools/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="3041e-112">`nuget add` Příkaz lze použít s jeden balíček současně, což může být nepohodlná při nastavování informační kanál s více balíčků.</span><span class="sxs-lookup"><span data-stu-id="3041e-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="3041e-113">V takových případech použít [ `nuget init` ](../tools/cli-ref-init.md) příkaz pro kopírování všech balíčků ve složce do informačního kanálu jako, pokud jste spustili `nuget add` na každé z nich jednotlivě.</span><span class="sxs-lookup"><span data-stu-id="3041e-113">In such cases, use the [`nuget init`](../tools/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="3041e-114">Například následující příkaz zkopíruje všechny balíčky z `c:\packages` na hierarchický strom na `\\myserver\packages`:</span><span class="sxs-lookup"><span data-stu-id="3041e-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="3041e-115">Stejně jako u `add` příkazu `init` vytvoří složku pro každý identifikátor balíčku, z nichž každý obsahuje uvnitř složky číslo verze, což je vhodné balíčku.</span><span class="sxs-lookup"><span data-stu-id="3041e-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
