---
title: Specifikace rozhraní příkazového řádku NuGet
description: Referenční informace pro příkaz specifikace nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cd1dc66676898e2be1c64698886a5ba29a07f88f
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794148"
---
# <a name="spec-command-nuget-cli"></a>Specifikace příkazu (rozhraní příkazového řádku NuGet)

**Platí pro:** vytvoření balíčku &bullet; **podporované verze:** všechny

Generuje `.nuspec` soubor pro nový balíček. Spuštění ve stejné složce jako soubor projektu (`.csproj`, `.vbproj`, `.fsproj`), `spec` vytvoří tokenizovaná `.nuspec` souboru. Další informace najdete v tématu [vytvoření balíčku](../create-packages/creating-a-package.md).

## <a name="usage"></a>Použití

```cli
nuget spec [<packageID>] [options]
```

kde `<packageID>` je volitelný balíček identifikátoru Uložit `.nuspec` souboru.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| AssemblyPath | Určuje cestu k sestavení, které má používat pro metadata. |
| Platnost | Přepíše všechny existující `.nuspec` souboru. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí vyzve k zadání uživatele o vstup ani potvrzení. |
| Podrobnosti | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
