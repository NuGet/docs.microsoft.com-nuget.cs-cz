---
title: "Poznámky k verzi NuGet 2.8.6 přílohy | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "Poznámky k verzi pro NuGet 2.8.6 přílohy včetně – známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 2.8.6 přílohy poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dfd0a76967280cc6a16b37fe2b2a3362231fce5
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
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