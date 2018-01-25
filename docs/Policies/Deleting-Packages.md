---
title: "Odstranění balíčků NuGet z nuget.org | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Zásady pro unlisting balíčky z nuget.org; trvalé odstranění nepodporuje kromě při balíčky porušují jiné zásady."
keywords: "Odstranění balíčku NuGet, balíček NuGet unlisting, zakázané používá balíčků"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6169e46e55176757bc1ad471a3d80885cb50e403
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="deleting-packages"></a>Odstraněním balíčků

nuget.org nepodporuje trvalé odstranění balíčků. Tím by došlo k přerušení všechny projekty v závislosti na dostupnost balíčku, zejména s pracovními postupy sestavení, které zahrnují obnovení balíčků.

nuget.org nemá podporuje *unlisting* balíček, což lze provést na stránce Správa balíčku na webu. Neuvedené balíčky nezobrazí v nuget.org nebo ve Visual Studiu a se nezobrazí ve výsledcích hledání. Neuvedené balíčků, ale je stále možné stáhnout a nainstalovat pomocí čísla přesnou verzi, která podporuje obnovení balíčků. Kromě toho může neuvedené balíčky zjištěná stále v následujícím konkrétním scénářům:

- Obnovení pomocí plovoucí verzí balíčků (například `1.0.0-*`), pokud nejnovější dostupné balíček odpovídající omezení verze nebo závislost je balíček není uveden v seznamu.
- Replikace balíčků pomocí katalogu (jak katalogu také obsahuje neuvedené balíčků).

## <a name="exceptions"></a>Výjimky

Ve výjimečných případech například věci porušení autorských práv a potenciálně nebezpečný obsah balíčků můžete odstranit ručně týmem NuGet. Odeslání žádosti o podporu prostřednictvím [Galerie NuGet](http://www.nuget.org) ke spuštění procesu.

## <a name="prohibited-use"></a>Zakázané používání

Balíčky, které splnit některý z následujících kritérií nejsou povoleny ve veřejné galerii NuGet a bude odebrán okamžitě bez diskuzi. Balíček bude vlastníky, ale, informováni o odebrání.

- Obsahuje malwaru, adwaru nebo jakýkoli druh spyware.
- Jsou navrženy pro poškodit pracovní stanice pro vývojáře nebo jejich organizace.
- Porušuje autorská práva nebo porušuje licence.
- Obsahuje neplatný obsah.
- Jsou používány k přikrčené na identifikátory balíček, včetně balíčků, které obsahují nulové produktivní obsah. Balíčky musí obsahovat kód nebo vlastníci musí protihráči postoupit identifikátor někomu, kdo má ve skutečnosti produktu pro odeslání.
- Pokusí se provést akci, která je určený není explicitně udělat galerie.

Pokud zjistíte, balíček, který je v rozporu s některou z těchto položek, klikněte na tlačítko **oznámení zneužití** odkaz na stránku podrobností balíčku a odeslání zprávy.

Všimněte si, že tým NuGet a .NET Foundation si vyhrazuje právo kdykoli změnit tato kritéria.
