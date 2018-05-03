---
title: Poznámky k verzi NuGet 2.8.6 přílohy
description: Poznámky k verzi pro NuGet 2.8.6 přílohy včetně – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ee801a0edfe22888d65506cea557fd9c79dcf7bd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-286-release-notes"></a>Poznámky k verzi NuGet 2.8.6 přílohy

[Poznámky k verzi NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 poznámky k verzi](../release-notes/nuget-2.8.7.md)

Byl vydán NuGet 2.8.6 přílohy 20 července 2015 jako menší aktualizace našich 2.8.5 VSIX s některé cílové opravy a vylepšení pro podporu balíčky, které mohou být dodávány s podporou pro model vývoj Windows 10 UWP.

Tato verze rozšíření Správce balíčků NuGet poskytuje podporu pouze pro Visual Studio 2013.

V této verzi dialogové okno Správce balíčků NuGet bylo přidala se podpora:

* Zavedly UAP cílový Framework Přezdívka pro podporu vývoj aplikací pro Windows 10.
* Koncové body verze 3 protokolu NuGet
* Podpora pro [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) vlastnost protocolVersion atribut úložiště zdroje. Výchozí hodnota je 2.
* Návratem zpět do vzdáleného úložiště, pokud požadovaný balíček verze není k dispozici v místní mezipaměti