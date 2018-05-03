---
title: Poskytovatelé přihlašovacích údajů NuGet pro Visual Studio
description: Poskytovatelé přihlašovacích údajů NuGet ověřit pomocí informačních kanálů implementací rozhraní IVsCredentialProvider v rozšíření sady Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 740df87b0d663aac482d888e916662528ce27030
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Ověřování informační kanály v sadě Visual Studio s poskytovatelé přihlašovacích údajů NuGet

Rozšíření NuGet Visual Studio 3.6 + podporuje poskytovatelé přihlašovacích údajů, které umožňují NuGet pro práci s ověřené kanály.
Po instalaci poskytovatele přihlašovacích údajů NuGet pro Visual Studio rozšíření NuGet sady Visual Studio automaticky získat a aktualizujte přihlašovací údaje pro ověřený kanály podle potřeby.

Ukázka implementace lze nalézt v [ukázka VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

> [!Note]
> Poskytovatelé přihlašovacích údajů NuGet pro Visual Studio musí být nainstalován jako regulární rozšíření sady Visual Studio a bude vyžadovat [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (aktuálně ve verzi preview) nebo novější.
>
> Poskytovatelé přihlašovacích údajů NuGet pro Visual Studio fungovat pouze v sadě Visual Studio (ne ve dotnet obnovení nebo nuget.exe). Poskytovatelé přihlašovacích údajů s nuget.exe, najdete v části [nuget.exe poskytovatelé přihlašovacích údajů](nuget-exe-Credential-providers.md).

## <a name="available-nuget-credential-providers-for-visual-studio"></a>K dispozici poskytovatelé přihlašovacích údajů NuGet pro Visual Studio

Není součástí rozšíření Visual Studio NuGet poskytovatele přihlašovacích údajů pro podporu Visual Studio Team Services.

Rozšíření NuGet Visual Studio používá interní `VsCredentialProviderImporter` které také hledá poskytovatelé přihlašovacích údajů modulu plug-in. Tyto přihlašovací údaje modul plug-in zprostředkovatele musí být zjistitelný jako Export rozhraní MEF typu `IVsCredentialProvider`.

Poskytovatelé přihlašovacích údajů k dispozici modul plug-in patří:

- [MyGet Credential Provider for Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Vytvoření zprostředkovatele pověření NuGet pro Visual Studio

Rozšíření NuGet Visual Studio 3.6 + implementuje interní CredentialService, který slouží k získání přihlašovacích údajů. CredentialService má seznam zprostředkovatelů předdefinované a modul plugin přihlašovacích údajů. Dokud se získal přihlašovací údaje, zkusí se každý poskytovatel postupně.

Během získávání přihlašovacích údajů službu přihlašovacích údajů se pokusí poskytovatelé přihlašovacích údajů v uvedeném pořadí, zastavení, jakmile jsou získat přihlašovací údaje:

1. Přihlašovací údaje budou načtena z NuGet konfigurační soubory (pomocí integrovaných `SettingsCredentialProvider`).
1. Pokud je zdroj balíčku na Visual Studio Team Services, `VisualStudioAccountProvider` se použije.
1. Všichni ostatní poskytovatelé přihlašovacích údajů modulu plug-in vyzkouší se postupně.
1. Pokud bylo získáno žádné přihlašovací údaje ještě uživatel vyzve k zadání pověření v dialogu standardní základní ověřování.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementace IVsCredentialProvider.GetCredentialsAsync

Chcete-li vytvořit poskytovatele přihlašovacích údajů NuGet pro Visual Studio, vytvořte rozšíření Visual Studio, který zveřejňuje veřejné Export rozhraní MEF implementace `IVsCredentialProvider` typ a dodržuje zásady uvedených níže.

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

Ukázka implementace lze nalézt v [ukázka VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Musí být každý poskytovatel pověření NuGet pro Visual Studio:

1. Určí, zda může poskytnout přihlašovací údaje pro cílový identifikátor URI před zahájením získání přihlašovacích údajů. Pokud zprostředkovatele nelze zadat přihlašovací údaje pro cílové zdroj, pak by měla vrátit `null`.
1. Pokud zprostředkovatel zpracovávat požadavky pro cílový identifikátor URI, ale nelze zadat přihlašovací údaje, by měl být vyvolána výjimka.

Vlastní poskytovatel pověření NuGet pro Visual Studio musí implementovat `IVsCredentialProvider` rozhraní, které jsou k dispozici v [NuGet.VisualStudio balíček](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Vstupní parametr |Popis|
| ----------------|-----------|
| Identifikátor URI uri | Zdroj balíčku Uri, pro které se vyžadují přihlašovací údaje.|
| IWebProxy proxy | Webový proxy server pro použití při komunikaci v síti. Hodnota Null, pokud neexistuje žádné ověření proxy serverem, který je nakonfigurovaný. |
| BOOL isProxyRequest | Hodnota TRUE, pokud tento požadavek je získat pověření pro ověření proxy serveru. Pokud implementace není platná pro získání přihlašovacích údajů proxy, by měl vrátit hodnotu null. |
| BOOL isRetry | Hodnota TRUE, pokud se přihlašovací údaje byly dříve požadované pro tento identifikátor Uri, ale zadaná pověření neumožňuje autorizovaný přístup. |
| Neinteraktivní BOOL | V případě hodnoty true musí poskytovatel pověření potlačit všechny uživatelské výzvy a místo toho použít výchozí hodnoty. |
| CancellationToken cancellationToken | Tento token zrušení kontroly k určení, pokud operace s požadavkem na pověření byla zrušena. |

**Návratová hodnota**: implementace objektu přihlašovací údaje [ `System.Net.ICredentials` rozhraní](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
