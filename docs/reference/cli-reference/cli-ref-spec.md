---
title: NuGet CLI – příkaz specifikace
description: Odkaz na příkaz nuget.exe spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622561"
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
