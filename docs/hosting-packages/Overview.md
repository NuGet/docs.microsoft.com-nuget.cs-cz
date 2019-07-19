---
title: Přehled hostování vlastních kanálů NuGet
description: Přehled otevření pro hostování vlastních informačních kanálů nebo galerií balíčků NuGet buď místně, nebo vzdáleně.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 737b13be70de9aaa7dec7904d4c2a4ec494ef7b3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317556"
---
# <a name="hosting-your-own-nuget-feeds"></a>Hostování vlastních kanálů NuGet

Místo toho, aby byly balíčky veřejně dostupné, možná budete chtít uvolnit balíčky pouze do omezené cílové skupiny, jako je například vaše organizace nebo pracovní skupina. Některé společnosti navíc můžou chtít omezit to, které knihovny třetích stran můžou vývojáři používat, a tak tyto vývojáře nasměrovat z omezeného zdroje balíčků, ale nenuget.org.

Pro všechny takové účely podporuje NuGet nastavení zdrojů privátních balíčků následujícími způsoby:

- Místní kanál: Balíčky je možné jednoduše umístit do vhodné síťové sdílené složky, ideálně pomocí `nuget init` a `nuget add` k vytvoření hierarchické struktury složek (NuGet 3.3 +). Podrobnosti najdete v tématu [místní informační kanály](../hosting-packages/local-feeds.md).
- NuGet.Server: Balíčky jsou zpřístupněny prostřednictvím místního HTTP serveru. Podrobnosti najdete v tématu [NuGet. Server](../hosting-packages/nuget-server.md).
- Galerie NuGet: Balíčky se hostují na internetovém serveru pomocí [projektu galerie NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (GitHub.com). Galerie NuGet poskytuje správu uživatelů a funkce, jako je například rozsáhlé webové uživatelské rozhraní, které umožňuje prohledávat a prozkoumat balíčky v prohlížeči, podobně jako nuget.org.

K dispozici je také několik dalších produktů NuGet pro hostování, které podporují vzdálené privátní kanály, včetně následujících:

- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), který je také k dispozici v Team Foundation Server 2017 a novějším.
- [MyGet](http://myget.org)
- [ProGet](http://inedo.com/proget) z Inedo
- [Registr balíčku GitHubu](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [Server NuGet](http://nugetserver.net/), projekt komunity z Inedo
- [Server NuGet (Open Source)](http://nuget-server.net), open source implementace podobná Inedo serveru NuGet
- [LiGet](https://github.com/ai-traders/liget), open source implementace serveru NuGet v2, který běží na Kestrel v Docker
- [BaGet](https://github.com/loic-sharma/BaGet), open source implementace serveru NuGet v3, která je postavená na ASP.NET Core
- [Sleet](https://github.com/emgarten/sleet), open source generátor statických kanálů NuGet V3
- [Artifactory](https://www.jfrog.com/artifactory/) z JFrog.
- [Nexus](http://www.sonatype.org/nexus/) z Sonatype.
- [TeamCity](https://www.jetbrains.com/teamcity/) z JetBrains.

Bez ohledu na to, jakým způsobem jsou balíčky hostované, můžete k nim přistupovat tak, že je přidáte `NuGet.Config`do seznamu dostupných zdrojů v. To lze provést v aplikaci Visual Studio, jak je popsáno v části [zdroje balíčků](../consume-packages/install-use-packages-visual-studio.md#package-sources)nebo z příkazového [`nuget sources`](../reference/cli-reference/cli-ref-sources.md)řádku pomocí příkazu. Cestou ke zdroji může být cesta k místní složce, název sítě nebo adresa URL.
