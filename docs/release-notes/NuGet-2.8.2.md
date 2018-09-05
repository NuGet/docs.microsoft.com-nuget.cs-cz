---
title: Zpráva k vydání verze NuGet ve verzi 2.8.2
description: Zpráva k vydání verze pro NuGet ve verzi 2.8.2 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551145"
---
# <a name="nuget-282-release-notes"></a>Zpráva k vydání verze NuGet ve verzi 2.8.2

[Zpráva k vydání verze NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [poznámkách k verzi NuGet 2.8.3](../release-notes/nuget-2.8.3.md)

NuGet ve verzi 2.8.2 vydaná 22. května 2014.  Tato verze zahrnuty pouze změny příkazového řádku nuget.exe, balíček NuGet.Server a dalších balíčcích NuGet.  Vydání neobsahuje k aktualizované rozšíření sady Visual Studio nebo rozšíření nástroje WebMatrix.

## <a name="notable-updates"></a>Důležité aktualizace

Nejdůležitější aktualizace byly v příkazového řádku nuget.exe a NuGet.Server balíčku (pro kanály NuGet v místním prostředí).

### <a name="important-nugetexe-bug-fixes"></a>Opravy chyb důležité nuget.exe

1. [nuget.exe Push se nezdaří a udržuje opakování](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe nabízených neodesílá pověření základního ověřování správně](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe nabízených oznámení nebude postupujte podle dočasné přesměrování](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Oprava chyby důležité NuGet.Server

1. [Nesprávná hodnota IsAbsoluteLatestVersion vrácený NuGet.Server](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Balíčky se aktualizovaly

Příkazový řádek nuget.exe a NuGet.Server opravy se dodávají jako aktualizace balíčků NuGet.  Došlo k jiné balíčky se aktualizovaly s ve verzi 2.8.2 také.

Tady je seznam aktualizované balíčky:

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (balíčku, není rozšíření)

## <a name="all-changes"></a>Všechny změny
Došlo k 10 problémy zákazníky a vyřešené ve verzi. Úplný seznam pracovní položky opravených NuGet ve verzi 2.8.2, prosím zobrazení [NuGet sledování problémů pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
