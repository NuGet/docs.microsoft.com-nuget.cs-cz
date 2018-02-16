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
ms.openlocfilehash: 80b8f9a3b74030ffd3f1c7b784204d98be67d684
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2018
---
# <a name="mirror-command-nuget-cli"></a>příkaz zrcadlení (NuGet CLI)

**Platí pro:** balíček publikování &bullet; **podporované verze:** zastaralé v 3.2 +

Odráží balíček a jeho závislosti z zadaná zdrojová úložiště do cílového úložiště.

> [!NOTE]
> Chcete-li příkaz pro verze NuGet před 3.2, přejděte na [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)vyberte nejnovější stabilní verze, stáhněte si `NuGet.ServerExtensions.dll` a `Nuget-Signed.exe` na váš místní disk a přejmenování `Nuget-Signed.exe` na `nuget.exe`.

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
| ApiKey | Klíč rozhraní API pro cílové úložiště. Pokud není přítomný, ten zadat *%AppData%\NuGet\NuGet.Config* se používá. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| NoCache | NuGet bránit v použití balíčky z mezipaměti místního počítače. |
| Nedojde k žádné akci | Protokoly co provádějí, ale neprovádí akce; předpokládá úspěch pro operace push. |
| Předběžné verze | Obsahuje předběžné verze balíčků v zrcadlení operaci. |
| Zdroj | Seznam zdrojů balíčku pro zrcadlení. Pokud nejsou zadány žádné zdroje, těm, které jsou definované v *%AppData%\NuGet\NuGet.Config* se používají jako výchozí bude použit nuget.org-li zadán žádný. |
| Časový limit | Určuje časový limit v sekundách pro vkládání na server. Výchozí hodnota je 300 sekund (5 minut). |
| Version | Verze balíčku pro instalaci. Pokud není zadáno, je Zrcadleno na nejnovější verzi. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
