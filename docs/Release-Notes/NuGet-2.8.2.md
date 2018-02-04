---
title: "Poznámky k verzi NuGet ve verzi 2.8.2 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro NuGet ve verzi 2.8.2 včetně – známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet ve verzi 2.8.2 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f50bd1f0c981ef293a4d2ff425e0dffbdf58036c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-282-release-notes"></a>Poznámky k verzi 2.8.2 NuGet

[Poznámky k verzi NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 poznámky k verzi](../release-notes/nuget-2.8.3.md)

NuGet ve verzi 2.8.2 byla vydána 22 může 2014.  Tato verze zahrnuty pouze změny nuget.exe příkazového řádku, balíček NuGet.Server a dalších balíčcích NuGet.  Verze neobsahuje aktualizované rozšíření sady Visual Studio nebo rozšíření nástroje WebMatrix.

## <a name="notable-updates"></a>Upozorňují na důležité aktualizace

Nejdůležitějším aktualizace byly v nuget.exe příkazového řádku a NuGet.Server balíčku (pro vlastním hostováním kanály NuGet).

### <a name="important-nugetexe-bug-fixes"></a>Opravy chyb důležité nuget.exe

1. [nuget.exe nabízení selže a udržuje opakování](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe nabízené neodesílá pověření základního ověřování správně](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe nabízené nebude podle dočasné přesměrování](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Oprava chyby důležité NuGet.Server

1. [Nesprávná hodnota IsAbsoluteLatestVersion vrácený NuGet.Server](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Balíčky aktualizovat

Nuget.exe příkazového řádku a NuGet.Server oprav je dodávána jako aktualizace balíčků NuGet.  Došlo k jiným balíčkům aktualizováno také ve verzi 2.8.2.

Tady je seznam aktualizované balíčků:

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (balíčku, není rozšíření)

## <a name="all-changes"></a>Všechny změny
Nebyly 10 problémy řešeny v verze. Úplný seznam pracovní položky pevná ve NuGet ve verzi 2.8.2, prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
