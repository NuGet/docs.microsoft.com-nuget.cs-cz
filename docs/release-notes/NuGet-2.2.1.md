---
title: Zpráva k vydání verze NuGet 2.2.1
description: Zpráva k vydání verze pro NuGet 2.2.1 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550695"
---
# <a name="nuget-221-release-notes"></a>Zpráva k vydání verze NuGet 2.2.1

[Zpráva k vydání verze NuGet 2.2](../release-notes/nuget-2.2.md) | [zpráva k vydání verze NuGet 2.5](../release-notes/nuget-2.5.md)

15. února 2013 byla vydána NuGet 2.2.1.  Číslo verze rozšíření VS je 2.2.40116.9051.

## <a name="localization-refresh"></a>Lokalizace aktualizace
NuGet dodán jako součást sady Visual Studio 2012, byl plně lokalizované do angličtiny + 13 jiných jazycích.  Od té doby byly dodány NuGet 2.1, tak i 2.2 ale lokalizace kdyby byly aktualizovány.  Vydání verze NuGet 2.2.1 aktualizuje naše lokalizace.

Uživatelské rozhraní a konzolu Powershellu Nugetu jsou lokalizovány do následujících jazycích:

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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Šablony sady Visual Studio podporují více úložišť předinstalovaný balíček
Pokud na základě šablony sady Visual Studio, můžete správci balíčků NuGet [předinstalovat balíčky](../visual-studio-extensibility/visual-studio-templates.md) jako součást šablony.  Až doteď, tato funkce má omezení, že všechny balíčky potřebné k pocházet ze stejného zdroje.  Nuget 2.2.1 však může mít balíčky nainstalované z více úložišť (v rámci šablony, VSIX nebo složku na disku, které jsou definovány v registru).

Hlavní scénáře pro tuto funkci je vlastní šablony projektů ASP.NET.  Předinstalované balíčky, stahování balíčků z místního disku použít předdefinované šablony ASP.NET.  Nyní můžete vytvořit vlastní šablonu projektu ASP.NET, která využívá existující balíčky nainstalované pomocí technologie ASP.NET, ale přidání dalších balíčků NuGet do šablony.

## <a name="bug-fixes"></a>Opravy chyb
NuGet 2.2.1 obsahuje několik cílová opravy chyb. Seznam pracovních položek opravených NuGet 2.2.1 prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Známé problémy

Pokud rozšiřujete šablony projektů ASP.NET, všechna úložiště předinstalovaný balíček musí používat stejnou hodnotu pro `isPreunzipped` atribut.
