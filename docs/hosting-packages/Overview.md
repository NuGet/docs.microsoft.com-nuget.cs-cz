---
title: Přehled hostování vlastní kanály NuGet
description: Přehled se otevře pro hostování své vlastní informační kanály balíčků NuGet nebo v galeriích místně nebo vzdáleně.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 45d8a6557ee02998f3d12b128ee2dc4fd6ae48bb
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145589"
---
# <a name="hosting-your-own-nuget-feeds"></a>Hostování vlastní NuGet informační kanály

Místo toho veřejně dostupné balíčky, může být vhodné k uvolnění balíčky pouze určité cílové skupině, jako je například vaše organizace nebo pracovní skupině. Kromě toho některé společnosti chtít omezit které knihovny třetích stran vývojářů může použít a proto směrovat tyto vývojáře k vykreslení ze zdroje balíčku omezené spíše než nuget.org.

Pro tyto účely NuGet podporuje nastavení privátních zdrojů balíčků následujícími způsoby:

- Místní informační kanál: Balíčky jsou jednoduše umístěny ve vhodné síťové sdílené složce, v ideálním případě pomocí `nuget init` a `nuget add` vytvořit hierarchická struktura složek (NuGet 3.3 +). Podrobnosti najdete v tématu [místní informační kanály](../hosting-packages/local-feeds.md).
- NuGet.Server: Balíčky jsou k dispozici prostřednictvím místního serveru HTTP. Podrobnosti najdete v tématu [NuGet.Server](../hosting-packages/nuget-server.md).
- Galerie NuGet: Balíčky jsou hostované na serveru Internetu pomocí [projektu Galerie NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (webu github.com). Galerie NuGet obsahuje funkce, jako je rozsáhlé webové uživatelské rozhraní, které umožňuje vyhledávání a zkoumání balíčků z prohlížeče, podobně jako na nuget.org a správy uživatelů.

Existuje také několik NuGet hostování produkty, které podporují vzdálené privátní kanály, včetně následujících:

- [Azure artefakty](https://www.visualstudio.com/docs/package/nuget/publish), což je také k dispozici na Team Foundation Server 2017 a novější.
- [MyGet](http://myget.org)
- [ProGet](http://inedo.com/proget) z Inedo
- [NuGet Server](http://nugetserver.net/), projekt komunitních z Inedo
- [NuGet Server (Otevřít zdroj)](http://nuget-server.net), podobně jako NuGet Server Inedo na open source implementace
- [LiGet](https://github.com/ai-traders/liget), open source implementace NuGet V2 serveru, který běží na kestrel v dockeru
- [BaGet](https://github.com/loic-sharma/BaGet), open source implementace NuGet V3 server založená na technologii ASP.NET Core
- [Sleet](https://github.com/emgarten/sleet), generátor kanálu statické NuGet V3 open source
- [Artifactory](https://www.jfrog.com/artifactory/) z JFrog.
- [Nexus](http://www.sonatype.org/nexus/) z Sonatype.
- [TeamCity](https://www.jetbrains.com/teamcity/) od JetBrains.

Bez ohledu na to, jak balíčky jsou hostované, můžete k nim přistupovat jejich přidáním do seznamu dostupných zdrojů v `NuGet.Config`. To můžete udělat v sadě Visual Studio podle popisu v [zdroje balíčků](../tools/package-manager-ui.md#package-sources), nebo z příkazového řádku pomocí [ `nuget sources` ](../tools/cli-ref-sources.md). Cesta ke zdroji může být cesta místní složku, síťový název nebo adresu URL.
