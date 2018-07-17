---
title: Podpora rozhraní příkazového řádku NuGet dlouhé cesty
description: Referenční informace pro podporu dlouhé cesty nuget.exe
author: zhili1208
ms.author: lzhi
manager: rob
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 0119be3fd8fd6c2e06e0135de5e498e0730bb0cc
ms.sourcegitcommit: a76ecc58f41c2c5b3536ff4a3f3fcbdf5258177c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39072744"
---
# <a name="long-path-support-nuget-cli"></a>Podpora dlouhé cesty (rozhraní příkazového řádku NuGet)

**Platí pro:** všechny &bullet; **podporované verze:** 4.8 +

NuGet.exe 4,8 a novější podporují dlouhé cesty pro soubory a adresáře pro scénáře, jako je balíček, obnovení, instalace a většinu scénářů, které je třeba cesty k souborům.

## <a name="required-operating-system"></a>Požadovaný operační systém

-   Windows 10 (verze 1607 nebo novější)
-   Windows 10 (verze. července 2015 nebo verze 1511) je-li upgrade rozhraní .NET Framework verze 4.6.2 nebo novější.
-   Windows Server 2016 (všechny verze)

## <a name="enable-win32-long-paths-group-policy"></a>Povolení zásad skupiny "Win32 dlouhé cesty"

Jeden je potřeba povolit dlouhé cesty podporu v těchto systémech nastavením zásad skupiny.

Pomocí následujících kroků:
1. Spuštění **Editor zásad skupiny** – zadejte "Upravit zásady skupiny" na vyhledávacím panelu spuštění nebo spuštění "gpedit.msc" pomocí příkazu Spustit (Windows-R).
2. V **Editor místních zásad skupiny**, povolte "místní počítač zásad nebo počítač platí následující konfigurace nebo správy šablony/všechny Win32 nastavení a povolit dlouhé cesty".

![Zásady dlouhé cesty](media/LongPathPolicy.png)


> [!Note]
> Povolení dalších nástrojů NuGet pro podporu dlouhé cesty
>
> -   Rozhraní příkazového řádku DotNet podporuje dlouhé cesty bez ohledu na operační systém nebo verzi.
> -   Visual Studio nebo nástroje msbuild/t: Restore zatím nepodporuje dlouhé cesty.
> -   Software, který používá NuGet knihoven ke spuštění obnovení a dalších příkazů, bude podporovat dlouhé cesty na stejných systémů, které NuGet.exe funguje na, pokud také nastavená longPathAware v jejich systému windows manifestu a nakonfigurovat UseLegacyPathHandling na hodnotu false pomocí souboru App.Config [ Další informace naleznete v tématu](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

