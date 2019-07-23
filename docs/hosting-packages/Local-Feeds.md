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
# <a name="local-feeds"></a>Místní informační kanály

Místní kanály balíčků NuGet jsou jednoduše hierarchické struktury složek v místní síti (nebo dokonce jenom v počítači), do kterých umístíte balíčky. Tyto kanály se pak dají použít jako zdroje balíčků se všemi ostatními operacemi NuGet pomocí rozhraní příkazového řádku, uživatelského rozhraní Správce balíčků a konzoly Správce balíčků.

Pokud chcete zdroj povolit, přidejte jeho cestu (například `\\myserver\packages`) do seznamu zdrojů pomocí [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) uživatelského rozhraní [Správce balíčků](../consume-packages/install-use-packages-visual-studio.md#package-sources) nebo příkazu.

> [!Note]
> Hierarchické struktury složek jsou podporovány v NuGet 3.3 +. Starší verze NuGet používají jenom jednu složku obsahující balíčky, jejichž výkon je mnohem menší než hierarchická struktura.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Inicializace a údržba hierarchických složek

Stromová struktura složky hierarchické verze má následující obecnou strukturu:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

NuGet tuto strukturu vytvoří automaticky, když použijete [`nuget add`](../reference/cli-reference/cli-ref-add.md) příkaz ke zkopírování balíčku do informačního kanálu:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

`nuget add` Příkaz funguje současně s jedním balíčkem, což může být nepraktické při vytváření informačního kanálu s více balíčky.

V takových případech použijte [`nuget init`](../reference/cli-reference/cli-ref-init.md) příkaz ke zkopírování všech balíčků do složky do informačního kanálu, jako kdyby byl každý z nich spuštěn `nuget add` samostatně. Například následující příkaz zkopíruje všechny balíčky z `c:\packages` do hierarchické stromové struktury na: `\\myserver\packages`

```cli
nuget init c:\packages \\myserver\packages
```

Stejně jako u `add` `init` příkazu vytvoří složku pro každý identifikátor balíčku, který obsahuje složku s číslem verze, v rámci které je příslušný balíček.
