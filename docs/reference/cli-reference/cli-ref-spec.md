---
title: NuGet CLI – příkaz specifikace
description: Odkaz na příkaz nuget.exe spec
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b7780ee5d2e722da5e1623f44709059dd9aa3d45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779153"
---
# <a name="spec-command-nuget-cli"></a>Spec – příkaz (NuGet CLI)

**Platí pro:** vytváření balíčků &bullet; **podporuje verze:** vše

Vygeneruje `.nuspec` soubor pro nový balíček. Pokud se spustí ve stejné složce jako soubor projektu ( `.csproj` , `.vbproj` , `.fsproj` ), `spec` vytvoří soubor s tokeny `.nuspec` . Další informace najdete v tématu [Vytvoření balíčku](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Využití

```cli
nuget spec [<packageID>] [options]
```

kde `<packageID>` je volitelný identifikátor balíčku, který se uloží do `.nuspec` souboru.

## <a name="options"></a>Možnosti

- **`-AssemblyPath`**

  Určuje cestu k sestavení, které se má použít pro metadata.

- **`-Force`**

  Přepíše všechny existující `.nuspec` soubory.


- **`-ForceEnglishOutput`**

  *(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.

- **`-?|-help`**

  Zobrazí informace o nápovědě k příkazu.

- **`-NonInteractive`**

  Potlačí výzvy pro vstup uživatele nebo potvrzení.

- **`-Verbosity [normal|quiet|detailed]`**

  Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
