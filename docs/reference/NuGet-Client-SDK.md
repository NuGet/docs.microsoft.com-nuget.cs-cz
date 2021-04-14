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
# <a name="nuget-client-sdk"></a>Sada SDK pro klienta NuGet

*Sada SDK klientské sady NuGet* odkazuje na skupinu balíčků NuGet:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) – Používá se k interakci s HTTP a souborovým kanálem NuGet na bázi souborů
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) – Používá se k interakci s balíčky NuGet. `NuGet.Protocol` závisí na tomto balíčku.

Zdrojový kód pro tyto balíčky najdete v úložišti [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) GitHub.
Zdrojový kód pro tyto příklady najdete v projektu [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) na GitHubu.

> [!Note]
> Dokumentaci k protokolu serveru NuGet najdete v tématu [rozhraní API serveru NuGet](~/api/overview.md).

## <a name="nugetprotocol"></a>NuGet. Protocol

Nainstalujte `NuGet.Protocol` balíček pro práci s informačními kanály balíčku NuGet na základě protokolu HTTP a složky:

```ps1
dotnet add package NuGet.Protocol
```

> [!Tip]
> `Repository.Factory` je definována v `NuGet.Protocol.Core.Types` oboru názvů a `GetCoreV3` Metoda je metoda rozšíření definovaná v `NuGet.Protocol` oboru názvů. Proto budete muset přidat `using` příkazy pro oba obory názvů.

### <a name="list-package-versions"></a>Výpis verzí balíčků

Vyhledá všechny verze Newtonsoft.Jsna základě [rozhraní API obsahu balíčku NuGet V3](../api/package-base-address-resource.md#enumerate-package-versions):

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Stažení balíčku

Stažení Newtonsoft.Jsna v 12.0.1 pomocí [rozhraní API obsahu balíčku NuGet V3](../api/package-base-address-resource.md):

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Získat metadata balíčku

Získejte metadata pro balíček "Newtonsoft.Json" pomocí [rozhraní API metadat balíčku NuGet V3](../api/registration-base-url-resource.md):

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Vyhledat balíčky

Vyhledejte balíčky "JSON" pomocí [rozhraní API pro vyhledávání NuGet V3](../api/search-query-service-resource.md):

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a>Vložení balíčku

Vložení balíčku pomocí [rozhraní API pro nabízené oznámení NuGet v3 a odstranit](../api/package-publish-resource.md):

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a>Odstranění balíčku

Odstranění balíčku pomocí [rozhraní API pro nabízené oznámení NuGet v3 a odstranit](../api/package-publish-resource.md):

> [!Note]
> Servery NuGet mají zdarma interpretovat požadavek na odstranění balíčku jako "pevné odstranění", "obnovitelné odstranění" nebo "zrušit seznam".
> Například nuget.org interpretuje požadavek na odstranění balíčku jako "unlist". Další informace o tomto postupu najdete v tématu [odstranění zásad balíčků](../nuget-org/policies/deleting-packages.md) .

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a>Práce s ověřenými informačními kanály

Použijte [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) pro práci s ověřenými informačními kanály.

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a>Balíčky NuGet. balení

Instalace `NuGet.Packaging` balíčku pro interakci se `.nupkg` soubory a `.nuspec` z datového proudu:

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a>Vytvoření balíčku

Vytvořte balíček, nastavte metadata a přidejte závislosti pomocí [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

> [!IMPORTANT]
> Důrazně doporučujeme, abyste balíčky NuGet vytvořili pomocí oficiálních nástrojů **NuGet a** nepoužívali toto rozhraní API nízké úrovně. K dispozici je celá řada vlastností, které jsou důležité pro balíček se správným formátem a nejnovější verzi nástrojů, které zahrnou tyto osvědčené postupy.
> 
> Další informace o vytváření balíčků NuGet najdete v tématu Přehled [pracovního postupu pro vytváření balíčků](../create-packages/overview-and-workflow.md) a dokumentaci k nástrojům pro oficiální balení (například [pomocí rozhraní příkazového řádku dotnet](../create-packages/creating-a-package-dotnet-cli.md)).

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a>Čtení balíčku

Přečtěte si balíček z datového proudu souboru pomocí [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

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
