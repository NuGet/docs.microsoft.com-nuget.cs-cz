---
title: Poznámky k verzi NuGet ve verzi 2.8.2
description: Poznámky k verzi pro NuGet ve verzi 2.8.2, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780363"
---
# <a name="nuget-282-release-notes"></a>Poznámky k verzi NuGet ve verzi 2.8.2

Poznámky k verzi [NuGet 2.8.1](../release-notes/nuget-2.8.1.md)  |  [Poznámky k verzi NuGet 2.8.3](../release-notes/nuget-2.8.3.md)

Ve verzi 2.8.2 NuGet byl vydán dne 22. května 2014.  Tato verze obsahuje jenom změny v nuget.exe příkazového řádku, balíček NuGet. Server a další balíčky NuGet.  Tato verze neobsahovala aktualizované rozšíření sady Visual Studio nebo rozšíření WebMatrix.

## <a name="notable-updates"></a>Významné aktualizace

Nejvýznamnější aktualizace byly v příkazovém řádku nuget.exe a balíčku NuGet. Server (pro informační kanály NuGet v místním prostředí).

### <a name="important-nugetexe-bug-fixes"></a>Důležité opravy chyb nuget.exe

1. [ Nahrávánínuget.exe se nezdařilo a pokračuje se opakováním](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe push neposílá správně pověření pro základní ověřování](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe nabízení oznámení nebude následovat po dočasném přesměrování](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Důležitá aktualizace NuGet. Server – oprava chyb

1. [NuGet. Server vrátil nesprávnou hodnotu IsAbsoluteLatestVersion.](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Aktualizované balíčky

Opravy nuget.exe příkazového řádku a NuGet. Server jsou dodávány jako aktualizace balíčků NuGet.  V ve verzi 2.8.2 byly také aktualizovány další balíčky.

Tady je seznam aktualizovaných balíčků:

1. [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet. CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet. Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (balíček, nikoli rozšíření)

## <a name="all-changes"></a>Všechny změny
V této verzi bylo vyřešeno 10 problémů. Úplný seznam pracovních položek opravených ve ve verzi 2.8.2 NuGet najdete v [přehledu problémů NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
