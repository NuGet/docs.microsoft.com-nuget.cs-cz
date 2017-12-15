---
title: "Poznámky k verzi 2.9 RC NuGet | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 04d76a22-63b0-41d1-9c27-799f4b35058f
description: "Poznámky k verzi pro NuGet 2.9 RC včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 2.9 k vydání verze RC, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 64b4cd17394ddb902c7101b9117039f381dc8488
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-29-rc-release-notes"></a>Poznámky k verzi 2.9 RC NuGet

[Poznámky k verzi NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 poznámky k verzi Preview](../release-notes/nuget-3.0-preview.md)

NuGet 2.9 byla vydána 10 září 2015 jako aktualizace 2.8.7 VSIX pro sadu Visual Studio 2012 a 2013.

### <a name="updates-in-this-release"></a>Aktualizace v této verzi

* Teď přeskočení balíčky zpracování, pokud jejich omezením `.nuspec` dokumentu je poškozený. - [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Opraveny multipartwebrequest zpracování \r\n pro scénáře, platformy Unix/Linux - [. 776](https://github.com/NuGet/Home/issues/776)
* Opravě integrace s událostí sestavení v sadě Visual Studio 2013 Community edition – [1180](https://github.com/NuGet/Home/issues/1180)


Úplný seznam opravách v této verzi najdete na Githubu v [2.8.8 milník](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
