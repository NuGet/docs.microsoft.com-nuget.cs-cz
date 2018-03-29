---
title: Příkaz delete NuGet rozhraní příkazového řádku | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro příkaz delete nuget.exe
keywords: nuget odstranit odkaz, odstraňte příkaz balíčku
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9445042c46ef41721def1fbbb8dcebf4afc14d1b
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="delete-command-nuget-cli"></a>Odstranit příkazu (NuGet CLI)

**Platí pro:** balíček publikování &bullet; **podporované verze:** všechny

Odstraní nebo unlists balíčku ze zdroje balíčku. Pro nuget.org, příkaz delete [unlists balíček](../policies/deleting-packages.md).

## <a name="usage"></a>Použití

```cli
nuget delete <packageID> <packageVersion> [options]
```

kde `<packageID>` a `<packageVersion>` přesný balíček odstranit nebo unlist identifikovat. Přesný postup závisí na zdroji. Pro místní složky, například daný balíček byl odstraněn; balíček není pro nuget.org neuvedené.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ApiKey | Klíč rozhraní API pro cílové úložiště. Pokud není přítomný, použije se verze zadaná v konfiguračním souboru. |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Zdroj | Určuje adresu URL serveru. Adresa URL nuget.org je `https://api.nuget.org/v3/index.json`. Pro privátní informační kanály, nahraďte název hostitele, například *%hostname%/api/v3*. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
