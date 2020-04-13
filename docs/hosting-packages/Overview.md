---
title: Přehled hosting u vlastních nugetových kanálů
description: Přehled otevře pro hostování vlastní nuget balíček kanály nebo galerie místně nebo vzdáleně.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 81acf15ac69d78d39d2784e77c18ba38bfea126d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "75385539"
---
# <a name="hosting-your-own-nuget-feeds"></a>Hostování vlastních nugetových kanálů

Místo zpřístupnění balíčků můžete uvolnit balíčky pouze omezené cílové skupině, například vaší organizaci nebo pracovní skupině. Kromě toho mohou některé společnosti chtít omezit knihovny třetích stran, které mohou vývojáři používat, a proto tyto vývojáře nasměrovat k tomu, aby čerpali z omezeného zdroje balíčků, nikoli nuget.org.

Pro všechny tyto účely NuGet podporuje nastavení soukromých zdrojů balíčků následujícími způsoby:

- Místní zdroj: Balíčky jsou jednoduše umístěny na `nuget init` vhodné `nuget add` sdílené síťové složky, v ideálním případě pomocí a vytvořit hierarchickou strukturu složek (NuGet 3.3+). Podrobnosti naleznete [v tématu Místní informační kanály](../hosting-packages/local-feeds.md).
- NuGet.Server: Balíčky jsou k dispozici prostřednictvím místního serveru HTTP. Podrobnosti naleznete v [tématu NuGet.Server](../hosting-packages/nuget-server.md).
- Galerie NuGet: Balíčky jsou hostovány na internetovém serveru pomocí [projektu Galerie NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com). NuGet Gallery poskytuje správu uživatelů a funkce, jako je například rozsáhlé webové uživatelské rozhraní, které umožňuje vyhledávání a zkoumání balíčků z prohlížeče, podobně jako nuget.org.

Existuje také několik dalších nugethostingových produktů, jako jsou [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) a [GitHub package registry,](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry) které podporují vzdálené soukromé kanály. Níže je uveden seznam těchto produktů:

- [Artefaktory](https://www.jfrog.com/artifactory/) z JFrog.
- [Artefakty Azure](https://www.visualstudio.com/docs/package/nuget/publish), které jsou taky dostupné na Team Foundation Server 2017 a novějším.
- [BaGet](https://github.com/loic-sharma/BaGet), open source implementace serveru NuGet V3 postavená na ASP.NET Core
- [Cloudsmith](https://cloudsmith.io/l/nuget-feed/), plně spravovaná správa balíčků SaaS
- [Registr balíčků GitHub](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [LiGet](https://github.com/ai-traders/liget), open source implementace serveru NuGet V2, který běží na poštolce v dockeru
- [MyGet](https://myget.org)
- [Nexus Úložiště OSS](https://www.sonatype.com/nexus-repository-oss) od Sonatype.
- [NuGet Server (Open Source)](https://github.com/svenkle/nuget-server), open source implementace podobná NuGet Serveru společnosti Inedo
- [NuGet Server](http://nugetserver.net/)– komunitní projekt společnosti Inedo
- [ProGet](https://inedo.com/proget) z Inedo
- [Sleet](https://github.com/emgarten/sleet)– generátor statického posuvu NuGet V3 s otevřeným zdrojovým kódem
- [TeamCity](https://www.jetbrains.com/teamcity/) z JetBrains.

Bez ohledu na to, jak jsou balíčky hostovány, k `NuGet.Config`nim přistupujete jejich přidáním do seznamu dostupných zdrojů v aplikaci . To lze provést v sadě Visual Studio, jak je popsáno v [balíček zdroje](../consume-packages/install-use-packages-visual-studio.md#package-sources)nebo z příkazového řádku pomocí [`nuget sources`](../reference/cli-reference/cli-ref-sources.md). Cesta ke zdroji může být cesta místní složky, název sítě nebo adresa URL.
