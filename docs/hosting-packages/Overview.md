---
title: Přehled hostování vlastních kanálů NuGet
description: Přehled otevření pro hostování vlastních informačních kanálů nebo galerií balíčků NuGet buď místně, nebo vzdáleně.
author: JonDouglas
ms.author: jodou
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 1b7bad6bcd897b746ea9eb6e89b80a88ee5e891a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774056"
---
# <a name="hosting-your-own-nuget-feeds"></a>Hostování vlastních kanálů NuGet

Místo toho, aby byly balíčky veřejně dostupné, možná budete chtít uvolnit balíčky pouze do omezené cílové skupiny, jako je například vaše organizace nebo pracovní skupina. Některé společnosti navíc můžou chtít omezit to, které knihovny třetích stran můžou vývojáři používat, a tak tyto vývojáře nasměrovat z omezeného zdroje balíčků, ale nenuget.org.

Pro všechny takové účely podporuje NuGet nastavení zdrojů privátních balíčků následujícími způsoby:

- Místní kanál: balíčky se jednoduše umísťují do vhodné síťové sdílené složky. v ideálním `nuget init` případě `nuget add` se pomocí a vytvoří hierarchická struktura složek (NuGet 3.3 +). Podrobnosti najdete v tématu [místní informační kanály](../hosting-packages/local-feeds.md).
- NuGet. Server: balíčky jsou zpřístupněny prostřednictvím místního HTTP serveru. Podrobnosti najdete v tématu [NuGet. Server](../hosting-packages/nuget-server.md).
- Galerie NuGet: balíčky se hostují na internetovém serveru pomocí [projektu galerie NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (GitHub.com). Galerie NuGet poskytuje správu uživatelů a funkce, jako je například rozsáhlé webové uživatelské rozhraní, které umožňuje prohledávat a prozkoumat balíčky v prohlížeči, podobně jako nuget.org.

K dispozici je také několik dalších produktů pro hostování NuGet, například [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) a [registr balíčků GitHubu](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry) , které podporují vzdálené privátní kanály. Níže je uvedený seznam těchto produktů:

- [Artifactory](https://www.jfrog.com/artifactory/) z JFrog.
- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), který je také k dispozici v Team Foundation Server 2017 a novějším.
- [BaGet](https://github.com/loic-sharma/BaGet), open source implementace serveru NuGet v3, která je postavená na ASP.NET Core
- [Cloudsmith](https://cloudsmith.io/l/nuget-feed/), plně spravovaná SaaS pro správu balíčků
- [Registr balíčku GitHubu](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [LiGet](https://github.com/ai-traders/liget), open source implementace serveru NuGet v2, který běží na Kestrel v Docker
- [MyGet](https://myget.org)
- [Nexus úložiště OSS](https://www.sonatype.com/nexus-repository-oss) ze Sonatype.
- [Server NuGet (Open Source)](https://github.com/svenkle/nuget-server), open source implementace podobná Inedo serveru NuGet
- [Server NuGet](http://nugetserver.net/), projekt komunity z Inedo
- [ProGet](https://inedo.com/proget) z Inedo
- [Sleet](https://github.com/emgarten/sleet), open source generátor statických kanálů NuGet V3
- [TeamCity](https://www.jetbrains.com/teamcity/) z JetBrains.

Bez ohledu na to, jakým způsobem jsou balíčky hostované, můžete k nim přistupovat tak, že je přidáte do seznamu dostupných zdrojů v `NuGet.Config` . To lze provést v aplikaci Visual Studio, jak je popsáno v části [zdroje balíčků](../consume-packages/install-use-packages-visual-studio.md#package-sources)nebo z příkazového řádku pomocí příkazu [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) . Cestou ke zdroji může být cesta k místní složce, název sítě nebo adresa URL.
