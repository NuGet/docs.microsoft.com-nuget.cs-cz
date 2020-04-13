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
# <a name="local-feeds"></a>Místní informační kanály

Místní NuGet balíček kanály jsou jednoduše hierarchické struktury složek v místní síti (nebo dokonce jen svůj vlastní počítač), ve kterém umístíte balíčky. Tyto kanály lze pak použít jako zdroje balíčků se všemi ostatními operacemi NuGet pomocí cli, ui Správce balíčků a konzoly Správce balíčků.

Chcete-li zdroj povolit, přidejte `\\myserver\packages`jeho cestu (například) do seznamu [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) zdrojů pomocí [uživatelského uživatelského nastavení Správce balíčků](../consume-packages/install-use-packages-visual-studio.md#package-sources) nebo příkazu.

> [!Note]
> Hierarchické struktury složek jsou podporovány v NuGet 3.3+. Starší verze NuGet použít pouze jednu složku obsahující balíčky, s jejichž výkon je mnohem nižší než hierarchické struktury.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Inicializace a údržba hierarchických složek

Hierarchický strom složek s verzí má následující obecnou strukturu:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

NuGet vytvoří tuto strukturu automaticky [`nuget add`](../reference/cli-reference/cli-ref-add.md) při použití příkazu ke kopírování balíčku do informačního kanálu:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

Příkaz `nuget add` pracuje s jedním balíčkem najednou, což může být nepohodlné při nastavování informačního kanálu s více balíčky.

V takových případech [`nuget init`](../reference/cli-reference/cli-ref-init.md) použijte příkaz ke zkopírování všech balíčků ve `nuget add` složce do informačního kanálu, jako byste běželi na každém z nich jednotlivě. Následující příkaz například zkopíruje `c:\packages` všechny balíčky z `\\myserver\packages`hierarchického stromu na :

```cli
nuget init c:\packages \\myserver\packages
```

Stejně `add` jako `init` u příkazu vytvoří složku pro každý identifikátor balíčku, z nichž každá obsahuje číselnou složku verze, ve které je příslušný balíček.
