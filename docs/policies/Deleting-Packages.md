---
title: Odstranění balíčků NuGet z nuget.org
description: Zásady pro unlisting balíčky z nuget.org; trvalé odstranění nepodporuje kromě při balíčky porušují jiné zásady.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 84a27c16968fa55ff1929db1adf98b8242a64fcf
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816981"
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
