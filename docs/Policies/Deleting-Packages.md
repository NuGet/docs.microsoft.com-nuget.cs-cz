---
title: "Odstranění balíčků NuGet z nuget.org | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a348ca2e-0a5d-40ad-ba33-9bb37e1d980b
description: "Zásady pro unlisting balíčky z nuget.org; trvalé odstranění nepodporuje kromě při balíčky porušují jiné zásady."
keywords: "Odstranění balíčku NuGet, balíček NuGet unlisting, zakázané používá balíčků"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 331979bdc3703ddbeff18e2bd0e6b0a17551e68b
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
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
- Pokus o galerii udělat něco není explicitně určené udělat.

Pokud zjistíte, balíček, který je v rozporu s některou z těchto položek, klikněte na tlačítko **oznámení zneužití** odkaz na stránku podrobností balíčku a odeslání zprávy.

Všimněte si, že tým NuGet a .NET Foundation si vyhrazuje právo kdykoli změnit tato kritéria.
