---
title: Požadavky na data uživatelů
description: Zásady pro vyžádání exportu a odstraňování uživatelských dat
author: JonDouglas
ms.author: jodou
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: e0ec429469a992c9558d1635890fd568398206a1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775726"
---
# <a name="user-data-requests"></a>Požadavky na data uživatelů

nuget.org uživatelé mohou odesílat žádosti o odstranění informací a žádosti o export informací prostřednictvím [NuGet.org](https://www.nuget.org). Oba typy jsou odesílány ve formě žádostí o podporu a správci nuget.org do 30 dnů.

Tato data uživatelů jsou přímo přístupná prostřednictvím nuget.org:

* Data týkající se účtu, jako je e-mailová adresa, účet přihlášení, profilový obrázek a nastavení e-mailových oznámení
* Vlastní klíče rozhraní API
* Seznam vlastněných balíčků

Tato data nejsou obsažena v datech exportovaných prostřednictvím žádosti o podporu.

## <a name="identifying-customer-data"></a>Identifikace zákaznických dat

Zákaznická data se dají identifikovat jako názvy uživatelských účtů nuget.org.

## <a name="deleting-customer-data"></a>Odstraňují se zákaznická data

Požadavek na odstranění uživatelských dat z nuget.org:

1. Uživatel se musí přihlásit k [NuGet.org](https://www.nuget.org) .
1. Uživatel musí odeslat žádost o odstranění účtu [NuGet.org/Account/Delete](https://www.nuget.org/account/delete) .

Uživatelům, kteří jsou jedinými vlastníky balíčků, doporučujeme najít nové vlastníky a teprve potom požádat o odstranění svého účtu. Pokud vlastnictví balíčku není předáno, balíček NuGet není v seznamu k dispozici a v důsledku toho již není k dispozici ve vyhledávacích dotazech v sadě Visual Studio nebo na webu nuget.org. Před odstraněním účtu můžou správci nuget.org pracovat s uživatelem, aby našli nové vlastníky pro balíčky, které vlastní.

Akci odstranění účtu dokončí správce nuget.org do 30 dnů od data žádosti.

Při odstranění účtu se všechna data uživatele odeberou ze systému nuget.org a provedou se následující akce:

* Odstraněné účty se neregistrují u nuget.org.
* Odstraní se všechny vlastněné klíče rozhraní API.
* Všechny rezervované obory názvů jsou vydané.
* Odstraní se všechna vlastnictví balíčku.

Vlastněné *balíčky se neodstraňují* . I když není seznam z výsledků hledání dostupný, zůstávají k dispozici prostřednictvím obnovení balíčků na projektech, které jsou na nich závislé.

## <a name="exporting-customer-data"></a>Export zákaznických dat

Po přihlášení do nuget.org může uživatel odeslat žádost o export prostřednictvím [NuGet.org/policies/Contact](https://www.nuget.org/policies/Contact) .

Exportovaná data jsou k dispozici po dobu 48 hodin uživateli ke stažení prostřednictvím objektu blob Azure. Po 48 hodinách vyprší platnost přístupu a uživatel musí podle potřeby Odeslat novou žádost o export.

Exportovaná data zahrnují:

* Žádosti o podporu pro uživatele
* Akce uživatele (publikovat balíček, vytvořit účet) jako trvalé v protokolech auditu
* Všechny informace o uživatelích jako trvalé v protokolech služby IIS
