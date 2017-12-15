---
title: "Příkaz delete NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: c213a07a-711d-47e0-9ee6-1d582e6cdb69
description: "Referenční dokumentace pro příkaz delete nuget.exe"
keywords: "nuget odstranit odkaz, odstraňte příkaz balíčku"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 92af9dc356f3932347864976496e0ba1216496c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="delete-command-nuget-cli"></a>Odstranit příkazu (NuGet CLI)

**Platí pro:** balíček publikování &bullet; **podporované verze:** všechny

Odstraní nebo unlists balíčku ze zdroje balíčku. Pro nuget.org, příkaz delete [unlists balíček](../policies/Deleting-Packages.md).

## <a name="usage"></a>Použití

```
nuget delete <packageID> <packageVersion> [options]
```

kde `<packageID>` a `<packageVersion>` přesný balíček odstranit nebo unlist identifikovat. Přesný postup závisí na zdroji. Pro místní složky, například daný balíček byl odstraněn; balíček není pro nuget.org neuvedené.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| apiKey | Klíč rozhraní API pro cílové úložiště. Pokud není přítomný, ten zadat *%AppData%\NuGet\NuGet.Config* se používá. |
| ConfigFile | *(2.5 +)*  NuGet konfiguračním souboru použít. Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Zdroj | Určuje adresu URL serveru. Adresa URL nuget.org je `https://api.nuget.org/v3/index.json`. Pro privátní informační kanály, nahraďte název hostitele, například *%hostname%/api/v3*. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné (2.5 +)*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
