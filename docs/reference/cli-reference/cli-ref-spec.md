---
title: NuGet CLI – příkaz specifikace
description: Referenční informace o příkazu NuGet. exe spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328273"
---
# <a name="spec-command-nuget-cli"></a>Spec – příkaz (NuGet CLI)

**Platí pro:** vytváření &bullet; balíčků **podporuje verze:** vše

Vygeneruje `.nuspec` soubor pro nový balíček. Pokud se spustí ve stejné složce jako soubor projektu (`.csproj`, `.vbproj`, `.fsproj`), `spec` vytvoří `.nuspec` soubor s tokeny. Další informace najdete v tématu [Vytvoření balíčku](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Použití

```cli
nuget spec [<packageID>] [options]
```

kde `<packageID>` je volitelný identifikátor balíčku, který se uloží `.nuspec` do souboru.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| AssemblyPath | Určuje cestu k sestavení, které se má použít pro metadata. |
| Ode | Přepíše všechny existující `.nuspec` soubory. |
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Help | Zobrazí informace o nápovědě k příkazu. |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Verbosity | Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
