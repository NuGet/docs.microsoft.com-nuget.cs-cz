---
title: "Nastavení místního kanály NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1354a527-d988-43d1-8dcf-6ce46ec5d3d4
description: "Jak vytvořit místní kanálu pro balíčky NuGet ve vaší místní síti pomocí složek"
keywords: "NuGet kanálu, galerie NuGet, místní balíček kanálu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32217622077ff983abaf00b2e6e5baf3064fff56
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="local-feeds"></a>Místní informační kanály

Místní kanály balíček NuGet se jednoduše hierarchické složky struktury v místní síti (nebo i právě svého počítače) ve které umístíte balíčky. Tyto kanály můžete potom použít jako zdroje balíčků s všechny operace NuGet pomocí rozhraní příkazového řádku, uživatelské rozhraní Správce balíčků a konzola Správce balíčků.

Povolit zdroj, přidejte její název cesty (například `\\myserver\packages`) do seznamu zdroje pomocí [uživatelského rozhraní Správce balíčků](../tools/package-manager-ui.md#package-sources) nebo [ `nuget sources` ](../tools/cli-ref-sources.md) příkaz.

> [!Note]
> Struktury hierarchické složky jsou podporovány v NuGet 3.3 +. Starší verze NuGet použijte pouze jednu složku obsahující balíčky, se kterými je mnohem nižší než hierarchická struktura výkonu.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Inicializace a údržbu hierarchické složek

Strom hierarchické verzí složek má následující obecné strukturu:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

NuGet tato struktura automaticky vytvoří při použití [ `nuget add` ](../tools/cli-ref-add.md) příkazu zkopírovat balíček do informačního kanálu:

```
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

`nuget add` Příkaz lze použít s jeden balíček současně, což může být nepohodlná při nastavování informační kanál s více balíčků.

V takových případech použít [ `nuget init` ](../tools/cli-ref-init.md) příkaz pro kopírování všech balíčků ve složce do informačního kanálu jako, pokud jste spustili `nuget add` na každé z nich jednotlivě. Například následující příkaz zkopíruje všechny balíčky z `c:\packages` na hierarchický strom na `\\myserver\packages`:

```
nuget init c:\packages \\myserver\packages
```

Stejně jako u `add` příkazu `init` vytvoří složku pro každý identifikátor balíčku, z nichž každý obsahuje uvnitř složky číslo verze, což je vhodné balíčku.
