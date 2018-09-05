---
title: Rozhraní příkazového řádku NuGet zrcadlový svazek
description: Referenční informace pro příkaz zrcadlení nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550203"
---
# <a name="mirror-command-nuget-cli"></a>Příkaz mirror (NuGet CLI)

**Platí pro:** balíček publikování &bullet; **podporované verze:** přestala nabízet v 3.2 +

Odráží balíček a jeho závislosti z úložišť zadaného zdroje do cílového úložiště.

> [!NOTE]
> Pokud chcete povolit tento příkaz pro verze NuGet před 3.2, přejděte na [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)vyberte nejnovější stabilní verzi, stáhněte si `NuGet.ServerExtensions.dll` a `Nuget-Signed.exe` na místní disk a přejmenování `Nuget-Signed.exe` k `nuget.exe`.

## <a name="usage"></a>Použití

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

kde `<packageID>` je balíček pro zrcadlení, nebo `<configFilePath>` identifikuje `packages.config` soubor, který uvádí balíčky pro zrcadlení.

`<listUrlTarget>` Určuje úložiště zdrojového kódu a `<publishUrlTarget>` určuje cílového úložiště.

Pokud je vaše cílové úložiště na `https://machine/repo` , na kterém běží [NuGet.Server](../hosting-packages/nuget-server.md), budou adresy URL seznamu a push `https://machine/repo/nuget` a `https://machine/repo/api/v2/package`v uvedeném pořadí.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ApiKey | Klíč rozhraní API pro cílového úložiště. Pokud není k dispozici, je uvedeno v konfiguračním souboru se používá (`%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| NoCache | Brání použití mezipaměti balíčků NuGet. Zobrazit [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NoOp | Protokoly, co by se dělalo, ale neprovede akce; předpokládá úspěchu operací push. |
| Platnost předběžné verze | Obsahuje předběžné verze balíčků v zrcadlení operace. |
| Zdroj | Seznam zdrojů balíčků pro zrcadlení. Pokud nejsou zadány žádné zdroje, těm, které jsou definovány v konfiguračním souboru (viz ApiKey výše) se používají, použije výchozí hodnotu nuget.org, pokud nejsou zadány žádné. |
| časový limit | Určuje časový limit v sekundách pro odesílání na server. Výchozí hodnota je 300 sekund (5 minut). |
| Version | Verze balíčku k instalaci. Pokud není zadán, je zrcadlena na nejnovější verzi. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
