---
title: Poznámky k verzi NuGet 2.2.1
description: Poznámky k verzi pro NuGet 2.2.1 včetně – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fddeb4e8c9fb2d85ba1876360862461e8ef025af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819290"
---
# <a name="nuget-221-release-notes"></a>Poznámky k verzi NuGet 2.2.1

[Poznámky k verzi NuGet 2.2](../release-notes/nuget-2.2.md) | [NuGet 2.5 poznámky k verzi](../release-notes/nuget-2.5.md)

NuGet 2.2.1 byla vydána 15. února 2013.  Číslo verze rozšíření sady Visual Studio je 2.2.40116.9051.

## <a name="localization-refresh"></a>Lokalizace aktualizace
NuGet dodávána jako součást sady Visual Studio 2012, byla plně lokalizované do angličtina + 13 další jazyky.  Od té doby byly součástí NuGet 2.1 a 2.2 ale lokalizace kdyby byla aktualizována.  Verze NuGet 2.2.1 aktualizuje naše lokalizace.

Lokalizace uživatelského rozhraní a prostředí PowerShell konzoly NuGet do následující jazyky:

1. Čínština (zjednodušená)
1. Čínština (tradiční)
1. Čeština
1. Angličtina
1. Francouzština
1. Němčina
1. Italština
1. Japonština
1. Korejština
1. Polština
1. Portugalština (Brazílie)
1. Ruština
1. Španělština
1. Turečtina

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Šablony sady Visual Studio podporují několik předinstalovaných balíček úložiště
Pokud můžete vytvořit šablony sady Visual Studio, můžete použít NuGet [předinstalovat balíčky](../visual-studio-extensibility/visual-studio-templates.md) v rámci šablony.  Až do této chvíle, tato funkce obsahovala omezení všech balíčků potřeby pocházet ze stejného zdroje.  U balíčku NuGet 2.2.1 ale může mít balíčky nainstalované z více úložiště (v šabloně, VSIX nebo složky na disku, které jsou definované v registru).

Hlavní scénáře pro tuto funkci je vlastní šablony projektů ASP.NET.  Předinstalované balíčky, stahování balíčků z místního disku použít předdefinované šablony ASP.NET.  Nyní můžete vytvořit vlastní šablony projektu ASP.NET, která používá existující balíčky nainstalované technologií ASP.NET, ale do šablony přidat další balíčky NuGet.

## <a name="bug-fixes"></a>Opravy chyb
NuGet 2.2.1 zahrnuje několik cílových opravy chyb. Seznam pracovní položky pevná ve NuGet 2.2.1, prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Známé problémy

Pokud jsou rozšíření šablony projektu ASP.NET, všechny úložiště předinstalované balíčku musíte použít stejné hodnoty `isPreunzipped` atribut.
