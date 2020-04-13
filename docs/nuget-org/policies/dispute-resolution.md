---
title: Řešení sporů názvů balíčků NuGet
description: Proces řešení sporů mezi vydavateli balíčků NuGet týkající se brandingu, ochranných známek a dalších konfliktních situací.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: a2f1fed578f1635296892ab925219f0f27883c02
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427497"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>Řešení sporů ohledně názvů balíčků NuGet

Tento článek poskytuje doporučený proces řešení pro členy komunity k řešení sporů s jinými vydavateli NuGet.

Předpokládejme například, že Northwind Traders vytvoří CRM systém, pro který poskytují ovladače klienta jako ke stažení MSI z jejich webových stránek. Nancy, nezávislý vývojář, chce usnadnit použití northwind klientské knihovny a změní ji `NorthwindTraders.Client`na balíček NuGet s názvem . Později Northwind chce vytvořit oficiální Balíček NuGet pro jejich vlastní pro jejich klientské knihovny, a proto by chtěli zpochybnit Nancy vlastnictví názvu balíčku.

V tomto scénáři Nancy nezdá se, že jedná se špatnými úmysly, ale spíše podporuje nástroje a zákazníky společnosti Northwind tím, že přispívá svým vlastním časem a kódem. Ve stejné době, Northwind je legitimní vlastník northwind jméno.

Podle níže uvedeného procesu mohou společnosti Northwind a Nancy spolupracovat na vhodném řešení, protože oba mají zájem sloužit komunitě vývojářů. Obvykle není nutné, aby se tým NuGet zapojil; spolupráce obvykle funguje nejlépe. Ve skutečnosti každý spor, který byl do týmu NuGet dosud upozorněn, byl vypracován bez nutnosti vynášet rozsudky.

## <a name="process"></a>Proces

1. Obraťte se na vlastníky balíčku máte spor s pomocí **kontaktu vlastníci** odkaz na stránce podrobnosti o balíčku. Vysvětlete svůj problém laskavým a přímým způsobem.
2. Odešlete kopii [support@nuget.org](mailto:support@nuget.org) zprávy tak, aby NuGet a .NET Foundation jsou si vědomi vašeho sporu.
3. Počkejte maximálně 30 dní na [support@nuget.org](mailto:support@nuget.org) řešení a poté jej znovu oznamte. Tým nuget.org podpory se zapojí a pokusí se vyřešit spor s oběma stranami.
