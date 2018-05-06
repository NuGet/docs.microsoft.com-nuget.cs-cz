---
title: Požadavky na Data uživatele
description: Exportovat zásady pro požadování uživatelská data a odstranit
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: 595a47da59c9b2672a10fc0f19e528c36a790134
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/04/2018
---
# <a name="user-data-requests"></a>Požadavky na Data uživatele

nuget.org uživatelé mohli odesílat žádosti o odstranění informace a požadavky na informace o exportu prostřednictvím [nuget.org](https://www.nuget.org). Oba typy jsou odeslány ve formě podporu požadavků a jsou provádět správce nuget.org do 30 dní.

Následující data uživatele je přímo přístupný prostřednictvím nuget.org:

* Souvisejícím s účtem data, jako jsou e-mailovou adresu, účet pro přihlášení, obrázek profilu a nastavení e-mailových oznámení
* Vlastní rozhraní API klíče
* Seznam balíčky, které vlastní

Tato data není součástí daty exportovanými pomocí žádosti o podporu.

## <a name="identifying-customer-data"></a>Identifikace data zákazníků

Zákaznická data je možné identifikovat jako nuget.org názvy uživatelských účtů.

## <a name="deleting-customer-data"></a>Odstraňování dat zákazníka

Žádost o odstraňuje data uživatele z nuget.org:

1. Uživatel musí přihlásit k [nuget.org](https://www.nuget.org)
1. Uživatel musí odeslat žádost o svůj účet odstranit [nuget.org/account/delete](https://www.nuget.org/account/delete)

Uživatelé, kteří jsou jedinou vlastníky balíčků doporučujeme najít nové vlastníky před výzvou tak, aby měl svůj účet odstranit. Pokud není přenést vlastnictví balíčku, je balíček NuGet neuvedené a v důsledku toho je již k dispozici v vyhledávací dotazy v sadě Visual Studio nebo na webu nuget.org. Před odstraněním účtu, správce nuget.org pracovat s uživatele k vyhledání nové vlastníků pro balíčky, které vlastní.

Akci odstranění účtu je dokončeno správce nuget.org do 30 dní od data požadavku.

Po odstranění účtu všechna data uživatele je odebrán ze systému nuget.org a budou provedeny následující akce:

* Odstraněného účtu stane registrace s nuget.org
* Všechny vlastněných že klíče rozhraní API se odstraní.
* Jsou vydávány všechny vyhrazené obory názvů
* Budou odebrány všechny vlastnictví balíčku

Vlastní balíčky jsou *není* odstranit. Když neuvedené z výsledků hledání, zůstanou k dispozici prostřednictvím balíčku obnovení do projektů, které jsou na nich závislé.

## <a name="exporting-customer-data"></a>Export dat zákazníka

Po přihlášení k nuget.org, uživatel může odeslat požadavek export prostřednictvím [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)

Data exportovaná je k dispozici pro 48 hodin pro uživatele o stažení prostřednictvím objektu Blob Azure. Po 48 hodinách přístup vyprší a uživatel musí odešlete novou žádost exportu, podle potřeby.

Exportovaná data zahrnuje:

* Požadavky na podporu uživatele
* Akce uživatele (publikování balíčku, vytvořte účet) jako trvalý v protokolech auditu
* Všechny informace o uživateli jako trvalý v protokoly služby IIS
