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
# <a name="nuget-client-sdk"></a>Sada SDK klienta NuGet

*Sada SDK klientské sady NuGet* odkazuje na skupinu balíčků NuGet:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) – používá se k interakci s http a souborovým kanálem NuGet na bázi souborů
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) – používá se k interakci s balíčky NuGet. `NuGet.Protocol` závisí na tomto balíčku.

Zdrojový kód pro tyto balíčky najdete v úložišti [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) GitHub.

> [!Note]
> Dokumentaci k protokolu serveru NuGet najdete v tématu [rozhraní API serveru NuGet](~/api/overview.md).

## <a name="getting-started"></a>Začínáme

### <a name="install-the-package"></a>Instalace balíčku

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a>Příklady

Tyto příklady najdete v projektu [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) na GitHubu.

### <a name="list-package-versions"></a>Výpis verzí balíčků

Vyhledejte všechny verze Newtonsoft. JSON pomocí [rozhraní API obsahu balíčku NuGet V3](../api/package-base-address-resource.md#enumerate-package-versions):

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Stažení balíčku

Stáhněte si Newtonsoft. JSON v 12.0.1 pomocí [rozhraní API obsahu balíčku NuGet V3](../api/package-base-address-resource.md):

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Získat metadata balíčku

Získejte metadata balíčku "Newtonsoft. JSON" pomocí [rozhraní API metadat balíčku NuGet V3](../api/registration-base-url-resource.md):

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Vyhledat balíčky

Vyhledejte balíčky "JSON" pomocí [rozhraní API pro vyhledávání NuGet V3](../api/search-query-service-resource.md):

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a>Dokumentace třetích stran

Příklady a dokumentaci k některému z rozhraní API najdete v následujících řadách blogu: Dave Glick, Published 2016:

- [Zkoumání knihoven NuGet v3, část 1: Úvod a koncepty](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Zkoumání knihoven NuGet v3, část 2: hledání balíčků](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Zkoumání knihoven NuGet v3, část 3: Instalace balíčků](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Tyto blogové příspěvky byly vypsány krátce po vydání verze **3.4.3** balíčků klientské sady SDK NuGet.
> Novější verze balíčků můžou být nekompatibilní s informacemi v blogových příspěvcích.

Martin Björkström obsahoval následující příspěvek blogu do série blogu Dave Glick, kde zavádí jiný přístup k instalaci balíčků NuGet pomocí klientské sady SDK NuGet:

- [Přenávštěva knihoven NuGet V3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
