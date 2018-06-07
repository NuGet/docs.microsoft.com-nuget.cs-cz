---
title: Specifikace příkaz NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro příkaz specifikace nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817083"
---
# <a name="spec-command-nuget-cli"></a>Specifikace příkazu (NuGet CLI)

**Platí pro:** balíček vytvoření &bullet; **podporované verze:** všechny

Generuje `.nuspec` soubor pro nový balíček. Pokud ve stejné složce jako soubor projektu (`.csproj`, `.vbproj`, `.fsproj`), `spec` vytvoří tokenizovaná `.nuspec` souboru. Další informace najdete v tématu [vytváření balíčku](../create-packages/creating-a-package.md).

## <a name="usage"></a>Použití

```cli
nuget spec [<packageID>] [options]
```

kde `<packageID>` je identifikátor volitelné balíček uložit v `.nuspec` souboru.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| AssemblyPath | Určuje cestu k sestavení, které má používat pro metadata. |
| Platnost | Přepíše všechny existující `.nuspec` souboru. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
