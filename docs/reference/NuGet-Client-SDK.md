---
title: Sada SDK klienta NuGet
description: Rozhraní API se vyvíjí a ještě není dokumentováno, ale příklady jsou k dispozici na blogu Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231237"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="23dbb-103">Sada SDK klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="23dbb-103">NuGet Client SDK</span></span>

<span data-ttu-id="23dbb-104">*Sada SDK klientské sady NuGet* odkazuje na skupinu balíčků NuGet:</span><span class="sxs-lookup"><span data-stu-id="23dbb-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="23dbb-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) – používá se k interakci s http a souborovým kanálem NuGet na bázi souborů</span><span class="sxs-lookup"><span data-stu-id="23dbb-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="23dbb-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) – používá se k interakci s balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="23dbb-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="23dbb-107">`NuGet.Protocol` závisí na tomto balíčku.</span><span class="sxs-lookup"><span data-stu-id="23dbb-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="23dbb-108">Zdrojový kód pro tyto balíčky najdete v úložišti [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) GitHub.</span><span class="sxs-lookup"><span data-stu-id="23dbb-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="23dbb-109">Dokumentaci k protokolu serveru NuGet najdete v tématu [rozhraní API serveru NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="23dbb-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="23dbb-110">Začínáme</span><span class="sxs-lookup"><span data-stu-id="23dbb-110">Getting started</span></span>

### <a name="install-the-package"></a><span data-ttu-id="23dbb-111">Instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="23dbb-111">Install the package</span></span>

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a><span data-ttu-id="23dbb-112">Příklady</span><span class="sxs-lookup"><span data-stu-id="23dbb-112">Examples</span></span>

<span data-ttu-id="23dbb-113">Tyto příklady najdete v projektu [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) na GitHubu.</span><span class="sxs-lookup"><span data-stu-id="23dbb-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="23dbb-114">Výpis verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="23dbb-114">List package versions</span></span>

<span data-ttu-id="23dbb-115">Vyhledejte všechny verze Newtonsoft. JSON pomocí [rozhraní API obsahu balíčku NuGet V3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="23dbb-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="23dbb-116">Stažení balíčku</span><span class="sxs-lookup"><span data-stu-id="23dbb-116">Download a package</span></span>

<span data-ttu-id="23dbb-117">Stáhněte si Newtonsoft. JSON v 12.0.1 pomocí [rozhraní API obsahu balíčku NuGet V3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="23dbb-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="23dbb-118">Získat metadata balíčku</span><span class="sxs-lookup"><span data-stu-id="23dbb-118">Get package metadata</span></span>

<span data-ttu-id="23dbb-119">Získejte metadata balíčku "Newtonsoft. JSON" pomocí [rozhraní API metadat balíčku NuGet V3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="23dbb-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="23dbb-120">Vyhledat balíčky</span><span class="sxs-lookup"><span data-stu-id="23dbb-120">Search packages</span></span>

<span data-ttu-id="23dbb-121">Vyhledejte balíčky "JSON" pomocí [rozhraní API pro vyhledávání NuGet V3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="23dbb-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a><span data-ttu-id="23dbb-122">Dokumentace třetích stran</span><span class="sxs-lookup"><span data-stu-id="23dbb-122">Third-party documentation</span></span>

<span data-ttu-id="23dbb-123">Příklady a dokumentaci k některému z rozhraní API najdete v následujících řadách blogu: Dave Glick, Published 2016:</span><span class="sxs-lookup"><span data-stu-id="23dbb-123">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="23dbb-124">Zkoumání knihoven NuGet v3, část 1: Úvod a koncepty</span><span class="sxs-lookup"><span data-stu-id="23dbb-124">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="23dbb-125">Zkoumání knihoven NuGet v3, část 2: hledání balíčků</span><span class="sxs-lookup"><span data-stu-id="23dbb-125">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="23dbb-126">Zkoumání knihoven NuGet v3, část 3: Instalace balíčků</span><span class="sxs-lookup"><span data-stu-id="23dbb-126">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="23dbb-127">Tyto blogové příspěvky byly vypsány krátce po vydání verze **3.4.3** balíčků klientské sady SDK NuGet.</span><span class="sxs-lookup"><span data-stu-id="23dbb-127">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="23dbb-128">Novější verze balíčků můžou být nekompatibilní s informacemi v blogových příspěvcích.</span><span class="sxs-lookup"><span data-stu-id="23dbb-128">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="23dbb-129">Martin Björkström obsahoval následující příspěvek blogu do série blogu Dave Glick, kde zavádí jiný přístup k instalaci balíčků NuGet pomocí klientské sady SDK NuGet:</span><span class="sxs-lookup"><span data-stu-id="23dbb-129">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="23dbb-130">Přenávštěva knihoven NuGet V3</span><span class="sxs-lookup"><span data-stu-id="23dbb-130">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
