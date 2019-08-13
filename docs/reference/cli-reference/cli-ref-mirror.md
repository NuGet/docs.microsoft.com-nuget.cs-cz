---
title: NuGet – příkaz zrcadlení CLI
description: Referenční informace o příkazu NuGet. exe Mirror
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959715"
---
# <a name="mirror-command-nuget-cli"></a>Příkaz mirror (NuGet CLI)

**Platí pro:** publikování &bullet; **podporovaných verzí balíčku:** zastaralé za 3.2 +

Zrcadlí balíček a jeho závislosti ze zadaných zdrojových úložišť do cílového úložiště.

> [!NOTE]
> Soubory NuGet. ServerExtensions. dll a NuGet-Signed. exe, které dříve podporovaly tento příkaz v NuGet 2. x (přejmenováním NuGet-Signed. exe na NuGet. exe), už nejsou k dispozici ke stažení. Pokud chcete použít příkaz podobný tomuto, vyzkoušejte [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).

## <a name="usage"></a>Použití

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

kde `<packageID>` je balíček k zrcadlení, nebo `<configFilePath>` identifikuje `packages.config` soubor, který vypisuje balíčky pro zrcadlení.

Určuje zdrojové úložiště a `<publishUrlTarget>` Určuje cílové úložiště. `<listUrlTarget>`

Pokud vaše cílové úložiště `https://machine/repo` používá službu [NuGet. Server](../../hosting-packages/nuget-server.md), bude seznam a adresy URL `https://machine/repo/nuget` nabízených oznámení a `https://machine/repo/api/v2/package`v uvedeném pořadí.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ApiKey | Klíč rozhraní API pro cílové úložiště Pokud není k dispozici, použije se ten zadaný v konfiguračním souboru (`%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Help | Zobrazí informace o nápovědě k příkazu. |
| NoCache | Zabraňuje balíčku NuGet v použití balíčků v mezipaměti. Viz [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NoOp | Protokoluje, co se provede, ale akce neprovádí. předpokládá úspěch pro operace push. |
| Předběžné verze | Zahrnuje předběžné verze balíčků v operaci zrcadlení. |
| Source | Seznam zdrojů balíčku pro zrcadlení. Pokud nejsou zadány žádné zdroje, budou použity ty, které jsou definovány v konfiguračním souboru (viz ApiKey výše). výchozí nastavení je nuget.org, pokud není zadáno. |
| časový limit | Určuje časový limit pro doručování na server v sekundách. Výchozí hodnota je 300 sekund (5 minut). |
| Version | Verze balíčku, který se má nainstalovat Pokud parametr není zadán, je zrcadlena nejnovější verze. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
