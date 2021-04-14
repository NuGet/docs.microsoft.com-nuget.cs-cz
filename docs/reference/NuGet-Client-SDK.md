---
title: Sada SDK pro klienta NuGet
description: Rozhraní API se vyvíjí a ještě není dokumentováno, ale příklady jsou k dispozici na blogu Dave Glick.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 6417c971dc13cf9ed05dcec4e4156af94c0ea058
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387384"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="5e132-103">Sada SDK pro klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="5e132-103">NuGet Client SDK</span></span>

<span data-ttu-id="5e132-104">*Sada SDK klientské sady NuGet* odkazuje na skupinu balíčků NuGet:</span><span class="sxs-lookup"><span data-stu-id="5e132-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="5e132-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) – Používá se k interakci s HTTP a souborovým kanálem NuGet na bázi souborů</span><span class="sxs-lookup"><span data-stu-id="5e132-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="5e132-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) – Používá se k interakci s balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="5e132-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="5e132-107">`NuGet.Protocol` závisí na tomto balíčku.</span><span class="sxs-lookup"><span data-stu-id="5e132-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="5e132-108">Zdrojový kód pro tyto balíčky najdete v úložišti [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) GitHub.</span><span class="sxs-lookup"><span data-stu-id="5e132-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="5e132-109">Zdrojový kód pro tyto příklady najdete v projektu [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) na GitHubu.</span><span class="sxs-lookup"><span data-stu-id="5e132-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="5e132-110">Dokumentaci k protokolu serveru NuGet najdete v tématu [rozhraní API serveru NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e132-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="5e132-111">NuGet. Protocol</span><span class="sxs-lookup"><span data-stu-id="5e132-111">NuGet.Protocol</span></span>

<span data-ttu-id="5e132-112">Nainstalujte `NuGet.Protocol` balíček pro práci s informačními kanály balíčku NuGet na základě protokolu HTTP a složky:</span><span class="sxs-lookup"><span data-stu-id="5e132-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

> [!Tip]
> <span data-ttu-id="5e132-113">`Repository.Factory` je definována v `NuGet.Protocol.Core.Types` oboru názvů a `GetCoreV3` Metoda je metoda rozšíření definovaná v `NuGet.Protocol` oboru názvů.</span><span class="sxs-lookup"><span data-stu-id="5e132-113">`Repository.Factory` is defined in the `NuGet.Protocol.Core.Types` namespace, and the `GetCoreV3` method is an extension method defined in the `NuGet.Protocol` namespace.</span></span> <span data-ttu-id="5e132-114">Proto budete muset přidat `using` příkazy pro oba obory názvů.</span><span class="sxs-lookup"><span data-stu-id="5e132-114">Therefore, you will need to add `using` statements for both namespaces.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="5e132-115">Výpis verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="5e132-115">List package versions</span></span>

<span data-ttu-id="5e132-116">Vyhledá všechny verze Newtonsoft.Jsna základě [rozhraní API obsahu balíčku NuGet V3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="5e132-116">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="5e132-117">Stažení balíčku</span><span class="sxs-lookup"><span data-stu-id="5e132-117">Download a package</span></span>

<span data-ttu-id="5e132-118">Stažení Newtonsoft.Jsna v 12.0.1 pomocí [rozhraní API obsahu balíčku NuGet V3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="5e132-118">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="5e132-119">Získat metadata balíčku</span><span class="sxs-lookup"><span data-stu-id="5e132-119">Get package metadata</span></span>

<span data-ttu-id="5e132-120">Získejte metadata pro balíček "Newtonsoft.Json" pomocí [rozhraní API metadat balíčku NuGet V3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="5e132-120">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="5e132-121">Vyhledat balíčky</span><span class="sxs-lookup"><span data-stu-id="5e132-121">Search packages</span></span>

<span data-ttu-id="5e132-122">Vyhledejte balíčky "JSON" pomocí [rozhraní API pro vyhledávání NuGet V3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="5e132-122">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="5e132-123">Vložení balíčku</span><span class="sxs-lookup"><span data-stu-id="5e132-123">Push a package</span></span>

<span data-ttu-id="5e132-124">Vložení balíčku pomocí [rozhraní API pro nabízené oznámení NuGet v3 a odstranit](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="5e132-124">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="5e132-125">Odstranění balíčku</span><span class="sxs-lookup"><span data-stu-id="5e132-125">Delete a package</span></span>

<span data-ttu-id="5e132-126">Odstranění balíčku pomocí [rozhraní API pro nabízené oznámení NuGet v3 a odstranit](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="5e132-126">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="5e132-127">Servery NuGet mají zdarma interpretovat požadavek na odstranění balíčku jako "pevné odstranění", "obnovitelné odstranění" nebo "zrušit seznam".</span><span class="sxs-lookup"><span data-stu-id="5e132-127">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="5e132-128">Například nuget.org interpretuje požadavek na odstranění balíčku jako "unlist".</span><span class="sxs-lookup"><span data-stu-id="5e132-128">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="5e132-129">Další informace o tomto postupu najdete v tématu [odstranění zásad balíčků](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="5e132-129">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="5e132-130">Práce s ověřenými informačními kanály</span><span class="sxs-lookup"><span data-stu-id="5e132-130">Work with authenticated feeds</span></span>

<span data-ttu-id="5e132-131">Použijte [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) pro práci s ověřenými informačními kanály.</span><span class="sxs-lookup"><span data-stu-id="5e132-131">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="5e132-132">Balíčky NuGet. balení</span><span class="sxs-lookup"><span data-stu-id="5e132-132">NuGet.Packaging</span></span>

<span data-ttu-id="5e132-133">Instalace `NuGet.Packaging` balíčku pro interakci se `.nupkg` soubory a `.nuspec` z datového proudu:</span><span class="sxs-lookup"><span data-stu-id="5e132-133">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="5e132-134">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="5e132-134">Create a package</span></span>

<span data-ttu-id="5e132-135">Vytvořte balíček, nastavte metadata a přidejte závislosti pomocí [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="5e132-135">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e132-136">Důrazně doporučujeme, abyste balíčky NuGet vytvořili pomocí oficiálních nástrojů **NuGet a** nepoužívali toto rozhraní API nízké úrovně.</span><span class="sxs-lookup"><span data-stu-id="5e132-136">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="5e132-137">K dispozici je celá řada vlastností, které jsou důležité pro balíček se správným formátem a nejnovější verzi nástrojů, které zahrnou tyto osvědčené postupy.</span><span class="sxs-lookup"><span data-stu-id="5e132-137">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="5e132-138">Další informace o vytváření balíčků NuGet najdete v tématu Přehled [pracovního postupu pro vytváření balíčků](../create-packages/overview-and-workflow.md) a dokumentaci k nástrojům pro oficiální balení (například [pomocí rozhraní příkazového řádku dotnet](../create-packages/creating-a-package-dotnet-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="5e132-138">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="5e132-139">Čtení balíčku</span><span class="sxs-lookup"><span data-stu-id="5e132-139">Read a package</span></span>

<span data-ttu-id="5e132-140">Přečtěte si balíček z datového proudu souboru pomocí [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="5e132-140">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="5e132-141">Dokumentace třetích stran</span><span class="sxs-lookup"><span data-stu-id="5e132-141">Third-party documentation</span></span>

<span data-ttu-id="5e132-142">Příklady a dokumentaci k některému z rozhraní API najdete v následujících řadách blogu: Dave Glick, Published 2016:</span><span class="sxs-lookup"><span data-stu-id="5e132-142">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="5e132-143">Zkoumání knihoven NuGet v3, část 1: Úvod a koncepty</span><span class="sxs-lookup"><span data-stu-id="5e132-143">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="5e132-144">Zkoumání knihoven NuGet v3, část 2: hledání balíčků</span><span class="sxs-lookup"><span data-stu-id="5e132-144">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="5e132-145">Zkoumání knihoven NuGet v3, část 3: Instalace balíčků</span><span class="sxs-lookup"><span data-stu-id="5e132-145">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="5e132-146">Tyto blogové příspěvky byly vypsány krátce po vydání verze **3.4.3** balíčků klientské sady SDK NuGet.</span><span class="sxs-lookup"><span data-stu-id="5e132-146">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="5e132-147">Novější verze balíčků můžou být nekompatibilní s informacemi v blogových příspěvcích.</span><span class="sxs-lookup"><span data-stu-id="5e132-147">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="5e132-148">Martin Björkström obsahoval následující příspěvek blogu do série blogu Dave Glick, kde zavádí jiný přístup k instalaci balíčků NuGet pomocí klientské sady SDK NuGet:</span><span class="sxs-lookup"><span data-stu-id="5e132-148">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="5e132-149">Přenávštěva knihoven NuGet V3</span><span class="sxs-lookup"><span data-stu-id="5e132-149">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
