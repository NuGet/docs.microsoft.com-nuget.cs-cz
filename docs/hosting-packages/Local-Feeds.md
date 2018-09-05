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
# <a name="local-feeds"></a>Místní informační kanály

Místní informační kanály balíčků NuGet se jednoduše hierarchickým struktur ve vaší místní síti (nebo jenom svého počítače) ve které umístíte balíčky. Tyto kanály můžete pak použít jako zdroje balíčků se všechny ostatní operace NuGet pomocí rozhraní příkazového řádku, uživatelské rozhraní Správce balíčků a konzole Správce balíčků.

Povolit zdroji, přidejte jeho cesta (například `\\myserver\packages`) do seznamu zdrojů pomocí [uživatelské rozhraní Správce balíčků](../tools/package-manager-ui.md#package-sources) nebo [ `nuget sources` ](../tools/cli-ref-sources.md) příkaz.

> [!Note]
> Hierarchickým struktury jsou podporovány ve Správci NuGet 3.3 +. Starší verze balíčku NuGet používat jenom jednu složku obsahující balíčky, s nimiž je mnohem nižší než hierarchickou strukturu výkonu.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Inicializace a udržování hierarchické složky

Strom hierarchických označené verzí složek má následující obecnou strukturu:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

NuGet tato struktura automaticky vytvoří při použití [ `nuget add` ](../tools/cli-ref-add.md) příkazu zkopírovat balíček do informačního kanálu:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

`nuget add` Příkaz funguje s jeden balíček současně, což může být nepraktické při nastavování informační kanál s více balíčky.

V takovém případě použijte [ `nuget init` ](../tools/cli-ref-init.md) příkazu pro kopírování všech balíčků ve složce do informačního kanálu, jako kdyby jste spustili `nuget add` na každé z nich samostatně. Například následující příkaz zkopíruje všechny balíčky z `c:\packages` hierarchické stromové struktury na `\\myserver\packages`:

```cli
nuget init c:\packages \\myserver\packages
```

Stejně jako u `add` příkazu `init` vytvoří složku pro každý balíček identifikátor, z nichž každý obsahuje složku číslo verze, ve kterém je příslušný balíček.
