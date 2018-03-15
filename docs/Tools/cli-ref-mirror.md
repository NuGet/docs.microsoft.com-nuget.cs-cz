---
title: "Příkaz zrcadlení NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro příkaz nuget.exe zrcadlení"
keywords: "referenční dokumentace zrcadlení nuget, příkaz zrcadlení"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0c1969cc04b2e2cead5e9dadf9739fdabdf65f6c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="mirror-command-nuget-cli"></a>příkaz zrcadlení (NuGet CLI)

**Platí pro:** balíček publikování &bullet; **podporované verze:** zastaralé v 3.2 +

Odráží balíček a jeho závislosti z zadaná zdrojová úložiště do cílového úložiště.

> [!NOTE]
> Chcete-li příkaz pro verze NuGet před 3.2, přejděte na [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)vyberte nejnovější stabilní verze, stáhněte si `NuGet.ServerExtensions.dll` a `Nuget-Signed.exe` na váš místní disk a přejmenování `Nuget-Signed.exe` k `nuget.exe`.

## <a name="usage"></a>Použití

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

kde `<packageID>` je balíček pro zrcadlení, nebo `<configFilePath>` identifikuje `packages.config` soubor, který obsahuje seznam balíčků pro zrcadlení.

`<listUrlTarget>` Určuje zdroj úložiště, a `<publishUrlTarget>` Určuje cíl úložiště.

Pokud vaše cílové úložiště na `https://machine/repo` na kterém běží [NuGet.Server](../hosting-packages/nuget-server.md), adresy URL seznamu a nabízených bude `https://machine/repo/nuget` a `https://machine/repo/api/v2/package`, v uvedeném pořadí.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ApiKey | Klíč rozhraní API pro cílové úložiště. Pokud není přítomný, verze zadaná v konfiguračním souboru se používá (`%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| NoCache | NuGet bránit v použití balíčky z mezipaměti místního počítače. |
| Nedojde k žádné akci | Protokoly co provádějí, ale neprovádí akce; předpokládá úspěch pro operace push. |
| Předběžné verze | Obsahuje předběžné verze balíčků v zrcadlení operaci. |
| Zdroj | Seznam zdrojů balíčku pro zrcadlení. Pokud nejsou zadány žádné zdroje, těm, které jsou definována v konfiguračním souboru (viz výše ApiKey) se používají, jako výchozí bude použit nuget.org-li zadán žádný. |
| Časový limit | Určuje časový limit v sekundách pro vkládání na server. Výchozí hodnota je 300 sekund (5 minut). |
| Version | Verze balíčku pro instalaci. Pokud není zadáno, je Zrcadleno na nejnovější verzi. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
