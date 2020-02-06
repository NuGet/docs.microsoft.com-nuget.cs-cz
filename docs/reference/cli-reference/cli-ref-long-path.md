---
title: Podpora dlouhých cest CLI NuGet
description: Referenční informace o podpoře dlouhých cest NuGet. exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 9b5a97d963eab7fbbde4aefae1c9b1a8bfcdeb11
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036952"
---
# <a name="long-path-support-nuget-cli"></a>Podpora dlouhých cest (rozhraní příkazového řádku NuGet)

**Platí pro:** všechny &bullet; **podporované verze:** 4,8 +

NuGet. exe 4,8 a novější podporuje dlouhé cesty k souborům a adresářům pro scénáře, jako jsou balíčky, obnovení, instalace a většina dalších scénářů, které potřebují cesty k souborům.

## <a name="required-operating-system"></a>Požadovaný operační systém

-   Windows 10 (verze 1607 nebo novější)
-   Windows 10 (verze z července 2015 nebo verze 1511) Pokud upgradujete .NET Framework na verze 4.6.2 nebo novější.
-   Windows Server 2016 (všechny verze)

## <a name="enable-win32-long-paths-group-policy"></a>Povolte "dlouhé cesty Win32" Zásady skupiny

Jedna z nich musí povolit podporu dlouhých cest v těchto systémech nastavením zásad skupiny.

Kroky:
1. Spusťte **Zásady skupiny editoru** – na panelu hledání spusťte příkaz upravit zásady skupiny nebo spusťte gpedit. msc z příkazu Run (Windows-R).
2. V **Editor místních zásad skupiny**povolte položku místní zásady počítače/Konfigurace počítače/šablony pro správu/všechna nastavení/Povolit dlouhé cesty Win32.

![Zásady dlouhých cest](media/LongPathPolicy.png)


> [!Note]
> Povolení dalších nástrojů NuGet pro podporu dlouhých cest
>
> -   Dotnet CLI podporuje dlouhé cesty bez ohledu na operační systém nebo verzi.
> -   Visual Studio nebo `msbuild -t:restore` ještě nepodporuje dlouhé cesty.
> -   Software, který používá knihovny NuGet ke spouštění obnovení a dalších příkazů, bude podporovat dlouhé cesty ke stejným systémům, na kterých pracuje NuGet. exe, pokud také nastavil `longPathAware` v manifestu Windows a nakonfiguroval `UseLegacyPathHandling` na `false` přes App. config [Zobrazit další informace](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

