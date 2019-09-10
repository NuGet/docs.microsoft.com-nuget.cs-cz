---
title: Přehled hostování vlastních kanálů NuGet
description: Přehled otevření pro hostování vlastních informačních kanálů nebo galerií balíčků NuGet buď místně, nebo vzdáleně.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 10651e2cc26f7df4115e4de5dac8c91c93af7374
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815300"
---
# <a name="hosting-your-own-nuget-feeds"></a>Hostování vlastních kanálů NuGet

Místo toho, aby byly balíčky veřejně dostupné, možná budete chtít uvolnit balíčky pouze do omezené cílové skupiny, jako je například vaše organizace nebo pracovní skupina. Některé společnosti navíc můžou chtít omezit to, které knihovny třetích stran můžou vývojáři používat, a tak tyto vývojáře nasměrovat z omezeného zdroje balíčků, ale nenuget.org.

Pro všechny takové účely podporuje NuGet nastavení zdrojů privátních balíčků následujícími způsoby:

- Místní kanál: Balíčky je možné jednoduše umístit do vhodné síťové sdílené složky, ideálně pomocí `nuget init` a `nuget add` k vytvoření hierarchické struktury složek (NuGet 3.3 +). Podrobnosti najdete v tématu [místní informační kanály](../hosting-packages/local-feeds.md).
- NuGet.Server: Balíčky jsou zpřístupněny prostřednictvím místního HTTP serveru. Podrobnosti najdete v tématu [NuGet. Server](../hosting-packages/nuget-server.md).
- Galerie NuGet: Balíčky se hostují na internetovém serveru pomocí [projektu galerie NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (GitHub.com). Galerie NuGet poskytuje správu uživatelů a funkce, jako je například rozsáhlé webové uživatelské rozhraní, které umožňuje prohledávat a prozkoumat balíčky v prohlížeči, podobně jako nuget.org.

K dispozici je také několik dalších produktů pro hostování NuGet, například [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) a [registr balíčků GitHubu](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry) , které podporují vzdálené privátní kanály. Níže je uvedený seznam těchto produktů:

- [Artifactory](https://www.jfrog.com/artifactory/) z JFrog.
- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), který je také k dispozici v Team Foundation Server 2017 a novějším.
- [BaGet](https://github.com/loic-sharma/BaGet), open source implementace serveru NuGet v3, která je postavená na ASP.NET Core
- [Cloudsmith](https://cloudsmith.io/l/nuget-feed/), plně spravovaná SaaS pro správu balíčků
- [Registr balíčku GitHubu](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [LiGet](https://github.com/ai-traders/liget), open source implementace serveru NuGet v2, který běží na Kestrel v Docker
- [MyGet](http://myget.org)
- [Nexus](http://www.sonatype.org/nexus/) z Sonatype.
- [Server NuGet (Open Source)](http://nuget-server.net), open source implementace podobná Inedo serveru NuGet
- [Server NuGet](http://nugetserver.net/), projekt komunity z Inedo
- [ProGet](http://inedo.com/proget) z Inedo
- [Sleet](https://github.com/emgarten/sleet), open source generátor statických kanálů NuGet V3
- [TeamCity](https://www.jetbrains.com/teamcity/) z JetBrains.

Bez ohledu na to, jakým způsobem jsou balíčky hostované, můžete k nim přistupovat tak, že je přidáte `NuGet.Config`do seznamu dostupných zdrojů v. To lze provést v aplikaci Visual Studio, jak je popsáno v části [zdroje balíčků](../consume-packages/install-use-packages-visual-studio.md#package-sources)nebo z příkazového [`nuget sources`](../reference/cli-reference/cli-ref-sources.md)řádku pomocí příkazu. Cestou ke zdroji může být cesta k místní složce, název sítě nebo adresa URL.
