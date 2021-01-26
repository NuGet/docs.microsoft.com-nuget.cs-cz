---
title: Poznámky k verzi NuGet 2.8.6
description: Poznámky k verzi pro NuGet 2.8.6, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776704"
---
# <a name="nuget-286-release-notes"></a>Poznámky k verzi NuGet 2.8.6

Poznámky k verzi [NuGet 2.8.5](../release-notes/nuget-2.8.5.md)  |  [Poznámky k verzi NuGet 2.8.7](../release-notes/nuget-2.8.7.md)

2.8.6 NuGet byl vydán 20. července 2015 jako dílčí aktualizace našeho 2.8.5 VSIX s některými cílenými opravami a vylepšení pro podporu balíčků, které mohou být dodávány s podporou pro vývojového modelu Windows 10 UWP.

Tato verze rozšíření Správce balíčků NuGet poskytuje podporu jenom pro Visual Studio 2013.

V této verzi bylo dialogové okno Správce balíčků NuGet přidáno pro:

* Zavedl (a) moniker cílového rozhraní UAP, který podporuje vývoj aplikací pro Windows 10.
* Verze 3 koncové body protokolu NuGet
* Podpora [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) atributu protocolVersion u zdrojů úložiště. Výchozí hodnota je "2".
* Návrat do vzdáleného úložiště, pokud není požadovaná verze balíčku k dispozici v místní mezipaměti