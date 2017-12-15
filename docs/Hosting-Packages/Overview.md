---
title: "Přehled hostování vlastní NuGet kanály | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 97577ddd-c294-432d-81a7-b4aebe88bd1c
description: "Přehled otevře pro hostování vlastní kanály balíček NuGet nebo Galerie místně nebo vzdáleně."
keywords: "NuGet kanálu, galerie NuGet vlastní balíček kanálu, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: c3c6b17cdeb4fe959adbc56bdc6ace73202a98fc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="hosting-your-own-nuget-feeds"></a>Hostování vlastní NuGet kanály

Místo provedení balíčky veřejně dostupné, můžete chtít verze balíčků jenom omezené cílové skupině, jako je vaše organizace nebo pracovní skupiny. Některé společnosti kromě toho může chtít omezit které třetích stran knihovny svého vývojáře může použít a proto přímé těchto vývojáři k vykreslení ze zdroje balíčku omezené spíše než nuget.org.

Pro tyto účely podporuje NuGet nastavení zdroje privátní balíčků následujícími způsoby:

- Místní kanál: balíčky jsou jednoduše umístit vhodný síťové sdílené složky, v ideálním případě pomocí `nuget init` a `nuget add` vytvořit hierarchickou strukturu složek (NuGet 3.3 +). Podrobnosti najdete v tématu [místní kanály](../hosting-packages/local-feeds.md).
- NuGet.Server: Balíčky jsou k dispozici prostřednictvím místní server HTTP. Podrobnosti najdete v tématu [NuGet.Server](../hosting-packages/NuGet-Server.md).
- Galerie NuGet: Balíčky jsou hostované na serveru Internetu pomocí [projektu Galerie NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (webu github.com). Správa uživatelů a funkce jako je například rozsáhlé webového uživatelského rozhraní, která umožňuje vyhledávání a zkoumání balíčky v prohlížeči, podobně jako nuget.org nabízí Galerie NuGet.

Existují také několik NuGet hostování produkty, které podporují vzdálené privátní informační kanály, včetně následujících:

- [Visual Studio Team Services balíček Management](https://www.visualstudio.com/docs/package/nuget/publish), což je také k dispozici na Team Foundation Server 2017 a novějším.
- [MyGet](http://myget.org)
- [ProGet](http://inedo.com/proget) z Inedo
- [NuGet Server](http://nugetserver.net/), komunity projekt z Inedo
- [NuGet serveru (zdroj otevřete)](http://nuget-server.net), podobně jako na Inedo NuGet Server open-source implementace
- [Artifactory](https://www.jfrog.com/artifactory/) z JFrog.
- [Nexus](http://www.sonatype.org/nexus/) z Sonatype.
- [TeamCity](https://www.jetbrains.com/teamcity/) z JetBrains.

Bez ohledu na to, jak jsou hostované balíčků, můžete je přístup jejich přidáním do seznamu dostupných zdrojů v `NuGet.Config`. To můžete provést v sadě Visual Studio podle popisu v [zdroje balíčků](../tools/package-manager-ui.md#package-sources), nebo z příkazového řádku pomocí [ `nuget sources` ](../tools/cli-ref-sources.md). Cesta ke zdroji může být místní složky pathname, síťový název nebo adresu URL.
