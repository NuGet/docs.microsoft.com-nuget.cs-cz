---
title: "Příkaz zrcadlení NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 190d7010-172e-44b8-8a32-94a2a63be4f3
description: "Referenční dokumentace pro příkaz nuget.exe zrcadlení"
keywords: "referenční dokumentace zrcadlení nuget, příkaz zrcadlení"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67daa1aa278b42b7974c562ba4097a525e7bb105
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="mirror-command-nuget-cli"></a>příkaz zrcadlení (NuGet CLI)

**Platí pro:** balíček publikování &bullet; **podporované verze:** zastaralé v 3.2 +

Odráží balíček a jeho závislosti z zadaná zdrojová úložiště do cílového úložiště.

> [!NOTE]
> Chcete-li příkaz pro verze NuGet před 3.2, přejděte na [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)vyberte nejnovější stabilní verze, stáhněte si `NuGet.ServerExtensions.dll` a `Nuget-Signed.exe` na váš místní disk a přejmenování `Nuget-Signed.exe` na `nuget.exe`.

## <a name="usage"></a>Použití

```
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

kde `<packageID>` je balíček pro zrcadlení, nebo `<configFilePath>` identifikuje `packages.config` soubor, který obsahuje seznam balíčků pro zrcadlení.

`<listUrlTarget>` Určuje zdroj úložiště, a `<publishUrlTarget>` Určuje cíl úložiště.

Pokud vaše cílové úložiště na `https://machine/repo` na kterém běží [NuGet.Server](../hosting-packages/NuGet-Server.md), adresy URL seznamu a nabízených bude `https://machine/repo/nuget` a `https://machine/repo/api/v2/package`, v uvedeném pořadí.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| apiKey | Klíč rozhraní API pro cílové úložiště. Pokud není přítomný, ten zadat *%AppData%\NuGet\NuGet.Config* se používá. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| NoCache | NuGet bránit v použití balíčky z mezipaměti místního počítače. |
| Nedojde k žádné akci | Protokoly co provádějí, ale neprovádí akce; předpokládá úspěch pro operace push. |
| Předběžné verze | Obsahuje předběžné verze balíčků v zrcadlení operaci. |
| Zdroj | Seznam zdrojů balíčku pro zrcadlení. Pokud nejsou zadány žádné zdroje, těm, které jsou definované v *%AppData%\NuGet\NuGet.Config* se používají jako výchozí bude použit nuget.org-li zadán žádný. |
| Časový limit | Určuje časový limit v sekundách pro vkládání na server. Výchozí hodnota je 300 sekund (5 minut). |
| Version | Verze balíčku pro instalaci. Pokud není zadáno, je Zrcadleno na nejnovější verzi. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
