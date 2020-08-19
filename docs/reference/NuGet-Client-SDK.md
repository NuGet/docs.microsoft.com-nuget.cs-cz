---
title: Sada SDK pro klienta NuGet
description: Rozhraní API se vyvíjí a ještě není dokumentováno, ale příklady jsou k dispozici na blogu Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 39a4de4071eec70c88a2add158f2a3a734f7d7b7
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622925"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="7b1c9-103">Sada SDK pro klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="7b1c9-103">NuGet Client SDK</span></span>

<span data-ttu-id="7b1c9-104">*Sada SDK klientské sady NuGet* odkazuje na skupinu balíčků NuGet:</span><span class="sxs-lookup"><span data-stu-id="7b1c9-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="7b1c9-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) – Používá se k interakci s HTTP a souborovým kanálem NuGet na bázi souborů</span><span class="sxs-lookup"><span data-stu-id="7b1c9-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="7b1c9-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) – Používá se k interakci s balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="7b1c9-107">`NuGet.Protocol` závisí na tomto balíčku.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="7b1c9-108">Zdrojový kód pro tyto balíčky najdete v úložišti [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) GitHub.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="7b1c9-109">Dokumentaci k protokolu serveru NuGet najdete v tématu [rozhraní API serveru NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b1c9-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="7b1c9-110">Začínáme</span><span class="sxs-lookup"><span data-stu-id="7b1c9-110">Getting started</span></span>

### <a name="install-the-packages"></a><span data-ttu-id="7b1c9-111">Nainstalovat balíčky</span><span class="sxs-lookup"><span data-stu-id="7b1c9-111">Install the packages</span></span>

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a><span data-ttu-id="7b1c9-112">Příklady</span><span class="sxs-lookup"><span data-stu-id="7b1c9-112">Examples</span></span>

<span data-ttu-id="7b1c9-113">Tyto příklady najdete v projektu [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) na GitHubu.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="7b1c9-114">Výpis verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="7b1c9-114">List package versions</span></span>

<span data-ttu-id="7b1c9-115">Vyhledá všechny verze Newtonsoft.Jsna základě [rozhraní API obsahu balíčku NuGet V3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="7b1c9-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="7b1c9-116">Stažení balíčku</span><span class="sxs-lookup"><span data-stu-id="7b1c9-116">Download a package</span></span>

<span data-ttu-id="7b1c9-117">Stažení Newtonsoft.Jsna v 12.0.1 pomocí [rozhraní API obsahu balíčku NuGet V3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="7b1c9-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="7b1c9-118">Získat metadata balíčku</span><span class="sxs-lookup"><span data-stu-id="7b1c9-118">Get package metadata</span></span>

<span data-ttu-id="7b1c9-119">Získejte metadata pro balíček "Newtonsoft.Json" pomocí [rozhraní API metadat balíčku NuGet V3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="7b1c9-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="7b1c9-120">Vyhledat balíčky</span><span class="sxs-lookup"><span data-stu-id="7b1c9-120">Search packages</span></span>

<span data-ttu-id="7b1c9-121">Vyhledejte balíčky "JSON" pomocí [rozhraní API pro vyhledávání NuGet V3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="7b1c9-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="create-a-package"></a><span data-ttu-id="7b1c9-122">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="7b1c9-122">Create a package</span></span>

<span data-ttu-id="7b1c9-123">Vytvořte balíček, nastavte metadata a přidejte závislosti pomocí [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="7b1c9-123">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b1c9-124">Důrazně doporučujeme, abyste balíčky NuGet vytvořili pomocí oficiálních nástrojů **NuGet a** nepoužívali toto rozhraní API nízké úrovně.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-124">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="7b1c9-125">K dispozici je celá řada vlastností, které jsou důležité pro balíček se správným formátem a nejnovější verzi nástrojů, které zahrnou tyto osvědčené postupy.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-125">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="7b1c9-126">Další informace o vytváření balíčků NuGet najdete v tématu Přehled [pracovního postupu pro vytváření balíčků](../create-packages/overview-and-workflow.md) a dokumentaci k nástrojům pro oficiální balení (například [pomocí rozhraní příkazového řádku dotnet](../create-packages/creating-a-package-dotnet-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="7b1c9-126">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="7b1c9-127">Čtení balíčku</span><span class="sxs-lookup"><span data-stu-id="7b1c9-127">Read a package</span></span>

<span data-ttu-id="7b1c9-128">Přečtěte si balíček z datového proudu souboru pomocí [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="7b1c9-128">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="7b1c9-129">Dokumentace třetích stran</span><span class="sxs-lookup"><span data-stu-id="7b1c9-129">Third-party documentation</span></span>

<span data-ttu-id="7b1c9-130">Příklady a dokumentaci k některému z rozhraní API najdete v následujících řadách blogu: Dave Glick, Published 2016:</span><span class="sxs-lookup"><span data-stu-id="7b1c9-130">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="7b1c9-131">Zkoumání knihoven NuGet v3, část 1: Úvod a koncepty</span><span class="sxs-lookup"><span data-stu-id="7b1c9-131">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="7b1c9-132">Zkoumání knihoven NuGet v3, část 2: hledání balíčků</span><span class="sxs-lookup"><span data-stu-id="7b1c9-132">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="7b1c9-133">Zkoumání knihoven NuGet v3, část 3: Instalace balíčků</span><span class="sxs-lookup"><span data-stu-id="7b1c9-133">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="7b1c9-134">Tyto blogové příspěvky byly vypsány krátce po vydání verze **3.4.3** balíčků klientské sady SDK NuGet.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-134">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="7b1c9-135">Novější verze balíčků můžou být nekompatibilní s informacemi v blogových příspěvcích.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-135">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="7b1c9-136">Martin Björkström obsahoval následující příspěvek blogu do série blogu Dave Glick, kde zavádí jiný přístup k instalaci balíčků NuGet pomocí klientské sady SDK NuGet:</span><span class="sxs-lookup"><span data-stu-id="7b1c9-136">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="7b1c9-137">Přenávštěva knihoven NuGet V3</span><span class="sxs-lookup"><span data-stu-id="7b1c9-137">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
