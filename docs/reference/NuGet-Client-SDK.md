---
title: Sada SDK klienta NuGet
description: Rozhraní API se vyvíjí a ještě není dokumentováno, ale příklady jsou k dispozici na blogu Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924608"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="fe295-103">Sada SDK klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="fe295-103">NuGet Client SDK</span></span>

<span data-ttu-id="fe295-104">*Sada SDK klienta NuGet* odkazuje na skupinu balíčků NuGet, které se nacentrují do [NuGet. Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet.](https://www.nuget.org/packages/NuGet.Packaging)Package a [NuGet. Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="fe295-104">The *NuGet Client SDK* refers to a group of NuGet packages centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="fe295-105">Tyto balíčky nahrazují předchozí knihovnu [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/) .</span><span class="sxs-lookup"><span data-stu-id="fe295-105">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

> [!Note]
>  <span data-ttu-id="fe295-106">Dokumentaci k protokolu serveru NuGet najdete v tématu [rozhraní API serveru NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe295-106">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="source-code"></a><span data-ttu-id="fe295-107">Zdrojový kód</span><span class="sxs-lookup"><span data-stu-id="fe295-107">Source code</span></span>

<span data-ttu-id="fe295-108">Zdrojový kód se zveřejňuje na GitHubu v projektu [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="fe295-108">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="fe295-109">Dokumentace třetích stran</span><span class="sxs-lookup"><span data-stu-id="fe295-109">Third-party documentation</span></span>

<span data-ttu-id="fe295-110">Příklady a dokumentaci k některému z rozhraní API najdete v následujících řadách blogu: Dave Glick, Published 2016:</span><span class="sxs-lookup"><span data-stu-id="fe295-110">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="fe295-111">Zkoumání knihoven NuGet v3, část 1: Úvod a koncepty</span><span class="sxs-lookup"><span data-stu-id="fe295-111">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="fe295-112">Zkoumání knihoven NuGet v3, část 2: hledání balíčků</span><span class="sxs-lookup"><span data-stu-id="fe295-112">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="fe295-113">Zkoumání knihoven NuGet v3, část 3: Instalace balíčků</span><span class="sxs-lookup"><span data-stu-id="fe295-113">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="fe295-114">Tyto blogové příspěvky byly vypsány krátce po vydání verze **3.4.3** balíčků klientské sady SDK NuGet.</span><span class="sxs-lookup"><span data-stu-id="fe295-114">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="fe295-115">Novější verze balíčků můžou být nekompatibilní s informacemi v blogových příspěvcích.</span><span class="sxs-lookup"><span data-stu-id="fe295-115">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="fe295-116">Martin Björkström obsahoval následující příspěvek blogu do série blogu Dave Glick, kde zavádí jiný přístup k používání klientské sady SDK NuGet pro instalaci balíčků NuGet:</span><span class="sxs-lookup"><span data-stu-id="fe295-116">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="fe295-117">Přenávštěva knihoven NuGet V3</span><span class="sxs-lookup"><span data-stu-id="fe295-117">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
