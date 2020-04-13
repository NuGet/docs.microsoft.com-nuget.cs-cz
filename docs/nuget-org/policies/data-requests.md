---
title: Požadavky na uživatelská data
description: Zásady pro vyžádání exportu a odstranění uživatelských dat
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427512"
---
# <a name="user-data-requests"></a>Požadavky na uživatelská data

nuget.org uživatelé mohou odesílat žádosti o odstranění informací a žádosti o export informací prostřednictvím [nuget.org](https://www.nuget.org). Oba typy jsou odeslány ve formě žádostí o podporu a jsou provedeny správci nuget.org do 30 dnů.

Následující uživatelská data jsou přímo přístupná prostřednictvím nuget.org:

* Údaje související s účtem, jako je e-mailová adresa, přihlašovací účet, profilový obrázek a nastavení e-mailových oznámení
* Vlastněné klíče ROZHRANÍ API
* Seznam vlastněných balíčků

Tato data nejsou zahrnuta v datech exportovaných prostřednictvím žádosti o podporu.

## <a name="identifying-customer-data"></a>Identifikace údajů o zákaznících

Údaje o zákaznících lze identifikovat jako nuget.org názvy uživatelských účtů.

## <a name="deleting-customer-data"></a>Odstranění dat zákazníků

Chcete-li požádat o odstranění uživatelských dat z nuget.org:

1. Uživatel se musí přihlásit k [nuget.org](https://www.nuget.org)
1. Uživatel musí odeslat žádost o odstranění svého účtu [nuget.org/account/delete](https://www.nuget.org/account/delete)

Uživatelům, kteří jsou výhradními vlastníky balíčků, doporučujeme najít nové vlastníky, než požádají o odstranění svého účtu. Pokud vlastnictví balíčku není převedena, balíček NuGet je neuvedena a v důsledku toho již není k dispozici ve vyhledávacích dotazech v sadě Visual Studio nebo na webu nuget.org. Před odstraněním účtu nuget.org správci spolupracují s uživatelem na hledání nových vlastníků pro balíčky, které vlastní.

Akci odstranění účtu dokončí správce nuget.org do 30 dnů od data žádosti.

Po odstranění účtu budou všechna data uživatele odebrána ze systému nuget.org a budou podniknuty následující akce:

* Odstraněný účet se stane neregistrovaným u nuget.org
* Všechny vlastněné klíče ROZHRANÍ API jsou odstraněny.
* Všechny vyhrazené obory názvů jsou uvolněny.
* Jakékoli vlastnictví balíčku bude odebráno.

Vlastněné balíčky *nejsou* odstraněny. Přestože nejsou uvedeny z výsledků hledání, zůstávají k dispozici prostřednictvím obnovení balíčku pro projekty, které jsou na nich závislé.

## <a name="exporting-customer-data"></a>Export dat zákazníků

Po přihlášení k nuget.org může uživatel odeslat žádost o export prostřednictvím [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)

Exportovaná data jsou k dispozici pro 48 hodin pro uživatele ke stažení prostřednictvím objektu blob Azure. Po 48 hodinách vyprší platnost přístupu a uživatel musí podle potřeby odeslat novou žádost o export.

Exportovaná data zahrnují:

* Požadavky uživatele na podporu
* Akce uživatele (publikovat balíček, vytvořit účet) jako trvalé v protokolech auditu
* Všechny informace o uživateli jako trvalé v protokolech iis
