---
title: Poznámky k verzi NuGet 2.2.1
description: Poznámky k verzi pro NuGet 2.2.1, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776804"
---
# <a name="nuget-221-release-notes"></a>Poznámky k verzi NuGet 2.2.1

Zpráva k [vydání verze](../release-notes/nuget-2.2.md)  |  NuGet 2,2 Zpráva k [vydání verze NuGet 2,5](../release-notes/nuget-2.5.md)

NuGet 2.2.1 byl vydán 15. února 2013.  Číslo verze rozšíření VS je 2.2.40116.9051.

## <a name="localization-refresh"></a>Aktualizace lokalizace
V případě, že je NuGet dodávána jako součást sady Visual Studio 2012, je plně lokalizována do jiných jazyků angličtina a 13.  Od té doby byly dodány balíčky NuGet 2,1 a 2,2, ale lokalizace nebyla obnovena.  Verze NuGet 2.2.1 aktualizuje naši lokalizaci.

Uživatelské rozhraní NuGet a konzole PowerShellu jsou lokalizované v následujících jazycích:

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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Šablony sady Visual Studio podporují více předinstalovaných úložišť balíčků
Pokud vytváříte šablony sady Visual Studio, můžete pomocí nástroje NuGet [předinstalovat balíčky](../visual-studio-extensibility/visual-studio-templates.md) jako součást šablony.  Do té doby měla tato funkce omezení, že všechny balíčky potřebné k tomu, aby se daly přijít ze stejného zdroje.  V případě NuGet 2.2.1a můžete mít balíčky nainstalované z několika úložišť (v šabloně, VSIX nebo složky na disku definovaném v registru).

Hlavním scénářem této funkce jsou vlastní šablony projektů ASP.NET.  Předdefinované šablony ASP.NET používají předinstalované balíčky a stahují balíčky z místního disku.  Nyní můžete vytvořit vlastní šablonu projektu ASP.NET, která používá existující balíčky nainstalované nástrojem ASP.NET, ale do šablony přidat další balíčky NuGet.

## <a name="bug-fixes"></a>Opravy chyb
NuGet 2.2.1 obsahuje několik cílových oprav chyb. Seznam pracovních položek opravených v NuGet 2.2.1 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Známé problémy

Pokud rozšiřujete šablony projektů ASP.NET, musí všechny předinstalované úložiště balíčků používat stejnou hodnotu `isPreunzipped` atributu.
