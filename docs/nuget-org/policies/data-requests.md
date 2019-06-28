---
title: Požadavky na Data uživatelů
description: Zásady žádosti o export dat uživatele a odstranit
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427512"
---
# <a name="user-data-requests"></a>Požadavky na Data uživatelů

nuget.org uživatelé mohli odesílat žádosti o odstranění informace a informace o žádosti o export prostřednictvím [nuget.org](https://www.nuget.org). Oba typy jsou odeslány ve formě podporu požadavků a jsou spustit správci nuget.org do 30 dní.

Následující data uživatele jsou přímo přístupné prostřednictvím nuget.org:

* Účet související data, jako jsou e-mailovou adresu, účet pro přihlášení, profilový obrázek a nastavení e-mailových oznámení
* Klíče vlastní rozhraní API
* Seznam balíčků vlastněná podnikem

Tato data není součástí data exportovaná prostřednictvím žádosti o podporu.

## <a name="identifying-customer-data"></a>Identifikace zákaznická data

Zákaznická data je možné identifikovat jako nuget.org názvy uživatelských účtů.

## <a name="deleting-customer-data"></a>Odstraňuje se zákaznická data

Žádost o odstranění uživatele data z webu nuget.org:

1. Uživatel musí přihlásit k [nuget.org](https://www.nuget.org)
1. Uživatel, musíte odeslat žádost pro svůj účet odstranit [nuget.org/account/delete](https://www.nuget.org/account/delete)

Uživatelé, kteří jsou výhradní vlastníci balíčky můžou najít novým vlastníkům před chce mít jeho účet odstraněn. Pokud nepřevezme vlastnictví balíčku, je balíček NuGet neuvedené v seznamu a v důsledku toho už nejsou k dispozici ve vyhledávacích dotazů v sadě Visual Studio nebo na webu nuget.org. Před odstraněním účtu, správce nuget.org pracovat uživatele o nalezení novým vlastníkům pro balíčky, které vlastní.

Účet akce odstranění dokončení správcem nuget.org do 30 dní od data požadavku.

Při odstraňování účtu všechna data uživatele se odebere ze systému nuget.org a budou provedeny následující akce:

* Odstraněný účet stane odregistrovat s nuget.org
* Všechny vlastněné, že klíče rozhraní API se odstraní.
* Všechny rezervované obory názvů jsou všeobecně dostupné
* Odeberou se všechny vlastnictví balíčku

Vlastní balíčky jsou *není* odstraněn. I když neuvedené ve výsledcích hledání, zůstaly dostupné prostřednictvím obnovení balíčků pro projekty, které jsou na nich závislé.

## <a name="exporting-customer-data"></a>Export zákaznických dat

Po přihlášení na nuget.org, uživatel může odeslat žádost o export prostřednictvím [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)

Data exportovaná je k dispozici po dobu 48 hodin na uživatele ke stažení prostřednictvím objektu Blob Azure. Po 48 hodinách přístup vyprší a uživatel musí odeslat novou žádost o export, podle potřeby.

Exportovaná data zahrnují:

* Žádostí o podporu uživatele
* Akce uživatele (publikování balíčku, vytvořte účet) jako trvalý v protokolech auditu
* Žádné informace o uživateli jako trvalý v protokolech služby IIS
