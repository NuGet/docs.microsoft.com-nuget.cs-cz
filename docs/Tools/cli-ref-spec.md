---
title: "Specifikace příkaz NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro příkaz specifikace nuget.exe"
keywords: "Specifikace odkaz nuget, specifikace příkaz"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
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
