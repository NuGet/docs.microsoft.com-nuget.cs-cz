---
title: Poskytovatelé přihlašovacích údajů Nugetu pro Visual Studio
description: Poskytovatelé přihlašovacích údajů Nugetu ověření pomocí informačních kanálů prostřednictvím implementace rozhraní IVsCredentialProvider v rozšíření sady Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e8d8ae22300b55b93badb65864163d959105dca2
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2018
ms.locfileid: "42793900"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Ověřování informačních kanálů v sadě Visual Studio prostřednictvím poskytovatelé přihlašovacích údajů Nugetu

Rozšíření NuGet Visual Studio 3.6 + podporuje poskytovatelé přihlašovacích údajů, které umožňují pracovat s ověřenými informačními kanály balíčků NuGet.
Po instalaci poskytovatele přihlašovacích údajů NuGet pro Visual Studio rozšíření NuGet sady Visual Studio automaticky načíst a aktualizovat přihlašovací údaje pro ověřené informační kanály podle potřeby.

Ukázková implementace lze nalézt v [ukázka VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Počínaje 4.8 + nová multiplatformní ověřování moduly plug-in také podporuje NuGet v sadě Visual Studio, ale nejsou doporučený postup z důvodů výkonu.

> [!Note]
> Poskytovatelé přihlašovacích údajů Nugetu pro Visual Studio musí být nainstalován jako rozšíření sady Visual Studio na regulární a bude vyžadovat [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) nebo vyšší.
>
> Poskytovatelé přihlašovacích údajů Nugetu pro Visual Studio fungují pouze v sadě Visual Studio (ne v dotnet restore nebo nuget.exe). Poskytovatelé přihlašovacích údajů s nuget.exe, naleznete v tématu [nuget.exe poskytovatelé přihlašovacích údajů](nuget-exe-Credential-providers.md).
> Přihlašovací údaje poskytovatelů v dotnet tak pro msbuild naleznete v tématu [NuGet pro různé platformy modulů plug-in](nuget-cross-platform-authentication-plugin.md)

## <a name="available-nuget-credential-providers-for-visual-studio"></a>K dispozici poskytovatelé přihlašovacích údajů Nugetu pro Visual Studio

Je integrované rozšíření Visual Studio NuGet poskytovatele přihlašovacích údajů pro podporu služby Visual Studio Team Services.

Rozšíření NuGet sady Visual Studio používá interní `VsCredentialProviderImporter` které rovněž vyhledává poskytovatelé modul plugin přihlašovacích údajů. Tito poskytovatelé přihlašovacích údajů modul plug-in musí být zjistitelné jako Export rozhraní MEF typu `IVsCredentialProvider`.

Poskytovatelé přihlašovacích údajů k dispozici modul plug-in patří:

- [MyGet Credential Provider for Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Vytvoření poskytovatele přihlašovacích údajů NuGet pro Visual Studio

Rozšíření NuGet Visual Studio 3.6 + implementuje interní CredentialService, který se používá k získání přihlašovacích údajů. CredentialService má seznam zprostředkovatelů integrované a modul plugin přihlašovacích údajů. Dokud se získat přihlašovací údaje, zkusí se každý poskytovatel postupně.

Při získání přihlašovacích údajů služba přihlašovacích údajů se pokusí poskytovatelé přihlašovacích údajů v uvedeném pořadí, zastavení, jako jsou přihlašovací údaje získat:

1. Přihlašovací údaje se načtou z NuGet konfiguračních souborů (použití předdefinované `SettingsCredentialProvider`).
1. Pokud je zdroj balíčků ve Visual Studio Team Services, `VisualStudioAccountProvider` se použije.
1. Všechny ostatní modulu plug-in Visual Studio poskytovatelé přihlašovacích údajů, vyzkouší se postupně.
1. Zkuste použít všechny NuGet pro různé platformy poskytovatelé přihlašovacích údajů postupně.
1. Pokud žádné přihlašovací údaje získat, ale uživateli zobrazí výzva k zadání přihlašovacích údajů a dialogové okno Standardní základní ověřování.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementace IVsCredentialProvider.GetCredentialsAsync

Chcete-li vytvořit poskytovatele přihlašovacích údajů NuGet pro Visual Studio, vytvořit rozšíření aplikace Visual Studio, která zveřejňuje veřejné Export rozhraní MEF implementace `IVsCredentialProvider` zadejte a dodržuje zásady uvedené níže.

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

Ukázková implementace lze nalézt v [ukázka VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Každý poskytovatel přihlašovacích údajů NuGet pro Visual Studio musí:

1. Určení, zda může poskytnout přihlašovací údaje pro cílový identifikátor URI před zahájením získání přihlašovacích údajů. Pokud zprostředkovatele nelze zadat přihlašovací údaje pro cílový zdroj, pak by měl vrátit `null`.
1. Pokud poskytovatel zpracovávat požadavky pro cílový identifikátor URI, ale nelze zadat přihlašovací údaje, by měl být vyvolána výjimka.

Musíte implementovat vlastní poskytovatele přihlašovacích údajů NuGet pro Visual Studio `IVsCredentialProvider` rozhraní, které jsou k dispozici v [NuGet.VisualStudio balíčku](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Vstupní parametr |Popis|
| ----------------|-----------|
| Identifikátor uri identifikátor URI | Zdroje balíčku Uri, pro které jsou požadovány přihlašovací údaje.|
| Rozhraní IWebProxy proxy | Webový proxy server při komunikaci v síti. Hodnota Null, pokud neexistuje žádné ověřování proxy server nakonfigurovaný. |
| BOOL isProxyRequest | True, pokud je tento požadavek se získat přihlašovací údaje pro ověření proxy serveru. Pokud implementace není platná pro získání přihlašovacích údajů proxy serveru, by měla být vrácena hodnota null. |
| BOOL isRetry | Hodnota TRUE, pokud pověření byla dříve vyžádána tento identifikátor Uri, ale zadaná pověření nepovolil autorizovaný přístup. |
| Neinteraktivní BOOL | Pokud je hodnota true, musí poskytovatele přihlašovacích údajů potlačit všechny uživatelské výzvy a místo toho použijte výchozí hodnoty. |
| CancellationToken cancellationToken | Tento token zrušení by měl být zkontrolována k určení, pokud žádost o přihlašovací údaje operace byla zrušena. |

**Návratová hodnota**: implementace objektu přihlašovací údaje [ `System.Net.ICredentials` rozhraní](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
