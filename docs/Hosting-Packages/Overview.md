---
title: "Přehled hostování vlastní NuGet kanály | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Přehled otevře pro hostování vlastní kanály balíček NuGet nebo Galerie místně nebo vzdáleně."
keywords: "NuGet kanálu, galerie NuGet vlastní balíček kanálu, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 628a36572846c652d648b45e0b18b63aac9a606e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="hosting-your-own-nuget-feeds"></a><span data-ttu-id="f2d31-104">Hostování vlastní NuGet kanály</span><span class="sxs-lookup"><span data-stu-id="f2d31-104">Hosting your own NuGet feeds</span></span>

<span data-ttu-id="f2d31-105">Místo provedení balíčky veřejně dostupné, můžete chtít verze balíčků jenom omezené cílové skupině, jako je vaše organizace nebo pracovní skupiny.</span><span class="sxs-lookup"><span data-stu-id="f2d31-105">Instead of making packages publicly available, you might want to release packages to only a limited audience, such as your organization or workgroup.</span></span> <span data-ttu-id="f2d31-106">Některé společnosti kromě toho může chtít omezit které třetích stran knihovny svého vývojáře může použít a proto přímé těchto vývojáři k vykreslení ze zdroje balíčku omezené spíše než nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f2d31-106">In addition, some companies may want to restrict which third-party libraries their developers may use, and thus direct those developers to draw from a limited package source rather than nuget.org.</span></span>

<span data-ttu-id="f2d31-107">Pro tyto účely podporuje NuGet nastavení zdroje privátní balíčků následujícími způsoby:</span><span class="sxs-lookup"><span data-stu-id="f2d31-107">For all such purposes, NuGet supports setting up private package sources in the following ways:</span></span>

- <span data-ttu-id="f2d31-108">Místní kanál: balíčky jsou jednoduše umístit vhodný síťové sdílené složky, v ideálním případě pomocí `nuget init` a `nuget add` vytvořit hierarchickou strukturu složek (NuGet 3.3 +).</span><span class="sxs-lookup"><span data-stu-id="f2d31-108">Local feed: Packages are simply placed on a suitable network file share, ideally using `nuget init` and `nuget add` to create a hierarchical folder structure (NuGet 3.3+).</span></span> <span data-ttu-id="f2d31-109">Podrobnosti najdete v tématu [místní kanály](../hosting-packages/local-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="f2d31-109">For details, see [Local Feeds](../hosting-packages/local-feeds.md).</span></span>
- <span data-ttu-id="f2d31-110">NuGet.Server: Balíčky jsou k dispozici prostřednictvím místní server HTTP.</span><span class="sxs-lookup"><span data-stu-id="f2d31-110">NuGet.Server: Packages are made available through a local HTTP server.</span></span> <span data-ttu-id="f2d31-111">Podrobnosti najdete v tématu [NuGet.Server](../hosting-packages/NuGet-Server.md).</span><span class="sxs-lookup"><span data-stu-id="f2d31-111">For details, see [NuGet.Server](../hosting-packages/NuGet-Server.md).</span></span>
- <span data-ttu-id="f2d31-112">Galerie NuGet: Balíčky jsou hostované na serveru Internetu pomocí [projektu Galerie NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (webu github.com).</span><span class="sxs-lookup"><span data-stu-id="f2d31-112">NuGet Gallery: Packages are hosted on an Internet server using the [NuGet Gallery Project](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span></span> <span data-ttu-id="f2d31-113">Správa uživatelů a funkce jako je například rozsáhlé webového uživatelského rozhraní, která umožňuje vyhledávání a zkoumání balíčky v prohlížeči, podobně jako nuget.org nabízí Galerie NuGet.</span><span class="sxs-lookup"><span data-stu-id="f2d31-113">NuGet Gallery provides user management and features such as an extensive web UI that allows searching and exploring packages from within the browser, similar to nuget.org.</span></span>

<span data-ttu-id="f2d31-114">Existují také několik NuGet hostování produkty, které podporují vzdálené privátní informační kanály, včetně následujících:</span><span class="sxs-lookup"><span data-stu-id="f2d31-114">There are also several other NuGet hosting products that support remote private feeds, including the following:</span></span>

- <span data-ttu-id="f2d31-115">[Visual Studio Team Services balíček Management](https://www.visualstudio.com/docs/package/nuget/publish), což je také k dispozici na Team Foundation Server 2017 a novějším.</span><span class="sxs-lookup"><span data-stu-id="f2d31-115">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), which is also available on Team Foundation Server 2017 and later.</span></span>
- [<span data-ttu-id="f2d31-116">MyGet</span><span class="sxs-lookup"><span data-stu-id="f2d31-116">MyGet</span></span>](http://myget.org)
- <span data-ttu-id="f2d31-117">[ProGet](http://inedo.com/proget) z Inedo</span><span class="sxs-lookup"><span data-stu-id="f2d31-117">[ProGet](http://inedo.com/proget) from Inedo</span></span>
- <span data-ttu-id="f2d31-118">[NuGet Server](http://nugetserver.net/), komunity projekt z Inedo</span><span class="sxs-lookup"><span data-stu-id="f2d31-118">[NuGet Server](http://nugetserver.net/), a community project from Inedo</span></span>
- <span data-ttu-id="f2d31-119">[NuGet serveru (zdroj otevřete)](http://nuget-server.net), podobně jako na Inedo NuGet Server open-source implementace</span><span class="sxs-lookup"><span data-stu-id="f2d31-119">[NuGet Server (Open Source)](http://nuget-server.net), an open-source implementation similar to Inedo's NuGet Server</span></span>
- <span data-ttu-id="f2d31-120">[Artifactory](https://www.jfrog.com/artifactory/) z JFrog.</span><span class="sxs-lookup"><span data-stu-id="f2d31-120">[Artifactory](https://www.jfrog.com/artifactory/) from JFrog.</span></span>
- <span data-ttu-id="f2d31-121">[Nexus](http://www.sonatype.org/nexus/) z Sonatype.</span><span class="sxs-lookup"><span data-stu-id="f2d31-121">[Nexus](http://www.sonatype.org/nexus/) from Sonatype.</span></span>
- <span data-ttu-id="f2d31-122">[TeamCity](https://www.jetbrains.com/teamcity/) z JetBrains.</span><span class="sxs-lookup"><span data-stu-id="f2d31-122">[TeamCity](https://www.jetbrains.com/teamcity/) from JetBrains.</span></span>

<span data-ttu-id="f2d31-123">Bez ohledu na to, jak jsou hostované balíčků, můžete je přístup jejich přidáním do seznamu dostupných zdrojů v `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="f2d31-123">Regardless of how packages are hosted, you access them by adding them to the list of available sources in `NuGet.Config`.</span></span> <span data-ttu-id="f2d31-124">To můžete provést v sadě Visual Studio podle popisu v [zdroje balíčků](../tools/package-manager-ui.md#package-sources), nebo z příkazového řádku pomocí [ `nuget sources` ](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="f2d31-124">This can be done in Visual Studio as described in [Package Sources](../tools/package-manager-ui.md#package-sources), or from the command line using [`nuget sources`](../tools/cli-ref-sources.md).</span></span> <span data-ttu-id="f2d31-125">Cesta ke zdroji může být místní složky pathname, síťový název nebo adresu URL.</span><span class="sxs-lookup"><span data-stu-id="f2d31-125">The path to a source can be a local folder pathname, a network name, or a URL.</span></span>
