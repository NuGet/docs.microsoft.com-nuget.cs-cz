---
title: Nastavení místních nugetových informačních kanálů
description: Jak vytvořit místní informační kanál pro balíčky NuGet pomocí složek v místní síti
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 42a5c30c058a9efb35338c1b484235b6ad111bd0
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "68317595"
---
# <a name="local-feeds"></a><span data-ttu-id="afc33-103">Místní informační kanály</span><span class="sxs-lookup"><span data-stu-id="afc33-103">Local feeds</span></span>

<span data-ttu-id="afc33-104">Místní NuGet balíček kanály jsou jednoduše hierarchické struktury složek v místní síti (nebo dokonce jen svůj vlastní počítač), ve kterém umístíte balíčky.</span><span class="sxs-lookup"><span data-stu-id="afc33-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="afc33-105">Tyto kanály lze pak použít jako zdroje balíčků se všemi ostatními operacemi NuGet pomocí cli, ui Správce balíčků a konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="afc33-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="afc33-106">Chcete-li zdroj povolit, přidejte `\\myserver\packages`jeho cestu (například) do seznamu [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) zdrojů pomocí [uživatelského uživatelského nastavení Správce balíčků](../consume-packages/install-use-packages-visual-studio.md#package-sources) nebo příkazu.</span><span class="sxs-lookup"><span data-stu-id="afc33-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md#package-sources) or the [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="afc33-107">Hierarchické struktury složek jsou podporovány v NuGet 3.3+.</span><span class="sxs-lookup"><span data-stu-id="afc33-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="afc33-108">Starší verze NuGet použít pouze jednu složku obsahující balíčky, s jejichž výkon je mnohem nižší než hierarchické struktury.</span><span class="sxs-lookup"><span data-stu-id="afc33-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="afc33-109">Inicializace a údržba hierarchických složek</span><span class="sxs-lookup"><span data-stu-id="afc33-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="afc33-110">Hierarchický strom složek s verzí má následující obecnou strukturu:</span><span class="sxs-lookup"><span data-stu-id="afc33-110">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="afc33-111">NuGet vytvoří tuto strukturu automaticky [`nuget add`](../reference/cli-reference/cli-ref-add.md) při použití příkazu ke kopírování balíčku do informačního kanálu:</span><span class="sxs-lookup"><span data-stu-id="afc33-111">NuGet creates this structure automatically when you use the [`nuget add`](../reference/cli-reference/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="afc33-112">Příkaz `nuget add` pracuje s jedním balíčkem najednou, což může být nepohodlné při nastavování informačního kanálu s více balíčky.</span><span class="sxs-lookup"><span data-stu-id="afc33-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="afc33-113">V takových případech [`nuget init`](../reference/cli-reference/cli-ref-init.md) použijte příkaz ke zkopírování všech balíčků ve `nuget add` složce do informačního kanálu, jako byste běželi na každém z nich jednotlivě.</span><span class="sxs-lookup"><span data-stu-id="afc33-113">In such cases, use the [`nuget init`](../reference/cli-reference/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="afc33-114">Následující příkaz například zkopíruje `c:\packages` všechny balíčky z `\\myserver\packages`hierarchického stromu na :</span><span class="sxs-lookup"><span data-stu-id="afc33-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="afc33-115">Stejně `add` jako `init` u příkazu vytvoří složku pro každý identifikátor balíčku, z nichž každá obsahuje číselnou složku verze, ve které je příslušný balíček.</span><span class="sxs-lookup"><span data-stu-id="afc33-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
