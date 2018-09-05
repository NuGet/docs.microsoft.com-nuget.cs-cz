---
title: Zpráva k vydání verze NuGet 2.8.6 přílohy
description: Zpráva k vydání verze pro NuGet 2.8.6 přílohy včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546488"
---
# <a name="nuget-286-release-notes"></a>Zpráva k vydání verze NuGet 2.8.6 přílohy

[Zpráva k vydání verze NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [zpráva k vydání verze NuGet 2.8.7](../release-notes/nuget-2.8.7.md)

Byla vydána NuGet 2.8.6 přílohy 20. července 2015 jako menší aktualizace našich 2.8.5 VSIX s některými cílová opravy a vylepšení pro podporu balíčky, které mohou být dodávány s podporou pro Windows 10 UPW vývojový model.

Tato verze rozšíření Správce balíčků NuGet poskytuje podporu pouze pro sadu Visual Studio 2013.

V této verzi má dialogové okno Správce balíčků NuGet přidány pro podporu:

* Zavedená Moniker cílového rozhraní UAP podporovat vývoj aplikací pro Windows 10.
* Koncové body NuGet protokolu verze 3
* Podpora pro [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) vlastnost protocolVersion atribut na zdrojích úložiště. Výchozí hodnota je "2"
* Návrat do vzdáleného úložiště, pokud požadovaný balíček verze není k dispozici v místní mezipaměti