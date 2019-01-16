---
title: Sada SDK pro klienta NuGet
description: Rozhraní API se rozvíjející a ještě zdokumentovaných, ale příklady jsou k dispozici na blogu Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 97ed3ec7d41d2847c0521af69373a1871eb585dd
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324679"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="b9446-103">Sada SDK pro klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="b9446-103">NuGet Client SDK</span></span>

> [!Note]
> <span data-ttu-id="b9446-104">Neměl by se zaměňovat s [NuGet *webové* rozhraní API](https://docs.microsoft.com/en-us/nuget/api/overview)</span><span class="sxs-lookup"><span data-stu-id="b9446-104">Not to be confused with the [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span></span>

<span data-ttu-id="b9446-105">*NuGet klientské sady SDK* odkazuje na skupinu soustředí na knihovny .NET [NuGet.Client](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), a [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="b9446-105">The *NuGet Client SDK* refers to a group of .NET libraries centered around [NuGet.Client](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="b9446-106">Tyto balíčky nahradit dříve [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) knihovny.</span><span class="sxs-lookup"><span data-stu-id="b9446-106">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

<span data-ttu-id="b9446-107">Pracujeme na s stabilní plochy, která může dokumentujeme brzy.</span><span class="sxs-lookup"><span data-stu-id="b9446-107">We are working on having a stable surface area that we can document soon.</span></span>

## <a name="source-code"></a><span data-ttu-id="b9446-108">Zdrojový kód</span><span class="sxs-lookup"><span data-stu-id="b9446-108">Source code</span></span>

<span data-ttu-id="b9446-109">Zdrojový kód se publikoval na Githubu v projektu [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="b9446-109">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="b9446-110">Dokumentace ke službě třetí strany</span><span class="sxs-lookup"><span data-stu-id="b9446-110">Third-party documentation</span></span>

<span data-ttu-id="b9446-111">Příklady a dokumentaci pro některé z rozhraní API najdete v následujících seriálech blogu podle Dave Glick, publikování 2016:</span><span class="sxs-lookup"><span data-stu-id="b9446-111">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="b9446-112">Zkoumání v3 knihovny NuGet, část 1: Úvod a koncepty</span><span class="sxs-lookup"><span data-stu-id="b9446-112">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="b9446-113">Zkoumání v3 knihovny NuGet, část 2: Vyhledávání balíčků</span><span class="sxs-lookup"><span data-stu-id="b9446-113">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="b9446-114">Zkoumání v3 knihovny NuGet, část 3: Instalace balíčků</span><span class="sxs-lookup"><span data-stu-id="b9446-114">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="b9446-115">Příspěvky na blogu byly napsány krátce po **3.4.3** verzi Nugetu, byly vydané balíčky sady SDK klienta.</span><span class="sxs-lookup"><span data-stu-id="b9446-115">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="b9446-116">Novější verze balíčků možná není kompatibilní s informacemi v blogových příspěvků.</span><span class="sxs-lookup"><span data-stu-id="b9446-116">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="b9446-117">Martin Björkström nebyla zpracování blogovém příspěvku k Dave Glick blogovou sérii, kde mu představuje jiný přístup na pomocí klientské sady SDK NuGet pro instalaci balíčků NuGet:</span><span class="sxs-lookup"><span data-stu-id="b9446-117">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="b9446-118">Byste nepřešli znovu na v3 knihovny NuGet</span><span class="sxs-lookup"><span data-stu-id="b9446-118">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
