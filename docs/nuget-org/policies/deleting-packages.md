---
title: Odstranění balíčků NuGet z webu nuget.org
description: Zásady pro unlisting balíčky z nuget.org; trvalé odstranění není podporováno s výjimkou při balíčky narušit jiné zásady.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 833f4a67bc75c5d650e85180b52ecd8f69218f15
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427509"
---
# <a name="deleting-packages"></a>Odstranění balíčků

nuget.org nepodporuje trvalé odstranění balíčků. Mohlo by narušil každý projekt v závislosti na dostupnost balíčku, zejména s pracovních postupech sestavení, které se týkají obnovení balíčků.

nuget.org nemá podporuje *unlisting* balíček, což lze provést na stránce Správa balíčků na webové stránce. Neuvedené v seznamu balíčků se nezobrazují na nuget.org nebo v Uživatelském rozhraní aplikace Visual Studio a ve výsledcích hledání nezobrazí. Neuvedené v seznamu balíčků, ale můžete dál stáhnout a nainstalovat pomocí čísla přesnou verzi, která podporuje obnovení balíčků. Kromě toho může neuvedené v seznamu balíčků zjištěné stále v těchto konkrétních scénářích:

- Obnovení pomocí plovoucí verze balíčků (například `1.0.0-*`), pokud je nejnovější dostupný balíček odpovídající omezení verze nebo závislost neuvedené v seznamu balíčků.
- Replikace balíčků prostřednictvím katalogu (jako v katalogu obsahuje také neuvedené v seznamu balíčků).

## <a name="exceptions"></a>Výjimky

Ve výjimečných případech například porušení autorských práv a potenciálně nebezpečný obsah balíčků můžete odstranit ručně týmu NuGet. Může hlásit balíček pomocí tlačítka "Ohlášení zneužití" na stránce s podrobnostmi balíčku NuGet.org. Pokud jste vlastník balíčku, přihlášení k účtu NuGet.org kontaktovat podporu NuGet pomocí tlačítka "Obraťte se na podporu" na stránce s podrobnostmi balíčku NuGet.org.

## <a name="prohibited-use"></a>Zakázané použití

Balíčky, které splnit některý z následujících kritérií nejsou povolené u veřejné Galerie NuGet a okamžitě odeberou bez diskuse. Balíček se vlastníci, ale, informováni o odebrání.

- Obsahuje malwaru, adwaru nebo jakýkoli druh spyware.
- Jsou navržené k jejich poškození pracovní stanici vývojáře nebo jejich organizace.
- Porušuje autorská práva nebo licence je v rozporu.
- Obsahuje neplatný obsah.
- Používají se k přikrčené na identifikátory balíček, včetně balíčků, které nemají žádnou produktivní obsah. Balíčky musí obsahovat kód nebo vlastníci musí protihráči postoupit identifikátor někomu, kdo má ve skutečnosti produktu k odeslání.
- Pokus o galerii, která je navržená nejsou explicitně udělat něco udělat.

Pokud zjistíte balíček, který je v rozporu s libovolnou z těchto položek, klikněte na tlačítko **ohlášení zneužití** odkaz na stránce s podrobnostmi balíčku a odeslat sestavu.

Všimněte si, že tým NuGet a .NET Foundation vyhrazuje právo kdykoli změnit tato kritéria.
