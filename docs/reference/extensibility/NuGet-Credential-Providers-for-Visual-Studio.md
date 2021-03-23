---
title: Poskytovatelé přihlašovacích údajů NuGetu pro Visual Studio
description: Poskytovatelé přihlašovacích údajů NuGet ověřují pomocí kanálů implementaci rozhraní IVsCredentialProvider v rozšíření sady Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: ab3bde0d320375f854a8f0a98fb90acfecf54aa3
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859093"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Ověřování informačních kanálů v aplikaci Visual Studio s poskytovateli přihlašovacích údajů NuGet

Rozšíření NuGet pro Visual Studio Extensions 3.6 + podporuje poskytovatele přihlašovacích údajů, což umožňuje, aby NuGet fungoval s ověřenými informačními kanály.
Po instalaci poskytovatele pověření NuGet pro Visual Studio rozšíření NuGet sady Visual Studio automaticky získá a obnoví přihlašovací údaje pro ověřené informační kanály podle potřeby.

Ukázkovou implementaci najdete v [ukázce VsCredentialProvider](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider).

V sadě Visual Studio NuGet používá interní, `VsCredentialProviderImporter` který také hledá poskytovatele přihlašovacích údajů modulu plug-in. Tito zprostředkovatelé přihlašovacích údajů modulu plug-in musí být zjistitelní jako export MEF typu `IVsCredentialProvider` .

Počínaje verzí 4,8 + NuGet v aplikaci Visual Studio je také podporováno nové moduly plug-in pro ověřování různých platforem, ale nejedná se o doporučený postup z hlediska výkonu.

> [!Note]
> Zprostředkovatelé pověření NuGet pro Visual Studio musí být nainstalováni jako běžné rozšíření sady Visual Studio a budou potřebovat [Visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) nebo vyšší.
>
> Zprostředkovatelé pověření NuGet pro Visual Studio fungují pouze v aplikaci Visual Studio (ne v dotnet restore nebo nuget.exe). Pro poskytovatele přihlašovacích údajů s nuget.exe si přečtěte téma [nuget.exe poskytovatelé přihlašovacích údajů](nuget-exe-Credential-providers.md).
> Pro poskytovatele přihlašovacích údajů v dotnet a MSBuild si přečtěte modul [Plug-in pro různé platformy](nuget-cross-platform-authentication-plugin.md)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Vytvoření poskytovatele pověření NuGet pro Visual Studio

Rozšíření NuGet pro Visual Studio Extension 3.6 + implementuje interní CredentialService, který se používá k získání přihlašovacích údajů. CredentialService má seznam integrovaných poskytovatelů přihlašovacích údajů a modulů plug-in. Každý poskytovatel se vyzkouší sekvenčně, dokud nebudou získány přihlašovací údaje.

Během získávání přihlašovacích údajů se služba přihlašovacích údajů pokusí poskytovatele přihlašovacích údajů vyzkoušet v následujícím pořadí a zastavuje se hned po získání přihlašovacích údajů:

1. Přihlašovací údaje se načítají z konfiguračních souborů NuGet (pomocí předdefinovaných `SettingsCredentialProvider` ).
1. Pokud je zdroj balíčku v Visual Studio Team Services, `VisualStudioAccountProvider` bude použit.
1. Všichni ostatní poskytovatelé přihlašovacích údajů sady Visual Studio budou zkoušet postupně.
1. Zkuste použít všechna poskytovatele přihlašovacích údajů pro různé platformy NuGet postupně.
1. Pokud se zatím nezískaly žádné přihlašovací údaje, zobrazí se uživateli výzva k zadání přihlašovacích údajů v dialogovém okně standardní základní ověřování.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementace IVsCredentialProvider. GetCredentialsAsync

Chcete-li vytvořit poskytovatele pověření NuGet pro Visual Studio, vytvořte rozšíření sady Visual Studio, které zveřejňuje veřejný export MEF implementující `IVsCredentialProvider` typ a dodržuje níže uvedené principy.

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

Ukázkovou implementaci najdete v [ukázce VsCredentialProvider](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider).

Každý poskytovatel pověření NuGet pro Visual Studio musí:

1. Před zahájením získání přihlašovacích údajů určete, jestli může poskytnout přihlašovací údaje pro cílový identifikátor URI. Pokud zprostředkovatel nemůže zadat přihlašovací údaje pro cílový zdroj, pak by měl vrátit `null` .
1. Pokud zprostředkovatel zpracovává požadavky pro cílový identifikátor URI, ale nemůže zadat přihlašovací údaje, měla by být vyvolána výjimka.

Vlastní zprostředkovatel pověření NuGet pro Visual Studio musí implementovat `IVsCredentialProvider` rozhraní dostupné v [balíčku NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Vstupní parametr |Popis|
| ----------------|-----------|
| Identifikátor URI URI | Identifikátor URI zdroje balíčku, pro který se vyžadují přihlašovací údaje.|
| Proxy IWebProxy | Webový proxy server, který se má použít při komunikaci v síti. Hodnota null, pokud není nakonfigurováno ověřování proxy serverem. |
| bool isProxyRequest | Hodnota true, pokud má tento požadavek získat přihlašovací údaje pro ověření proxy serveru. Pokud implementace není platná pro získání přihlašovacích údajů proxy serveru, měla by být vrácena hodnota null. |
| logická akce | True, pokud se pro tento identifikátor URI dřív požadovaly přihlašovací údaje, ale zadané přihlašovací údaje nepovolovaly autorizovaný přístup. |
| bool neinteraktivní | Pokud je hodnota true, poskytovatel pověření musí potlačit všechny výzvy uživatelů a místo toho použít výchozí hodnoty. |
| CancellationToken cancellationToken | Tento token zrušení by měl být zkontrolován, aby bylo možné zjistit, zda operace požadující přihlašovací údaje byla zrušena. |

**Návratová hodnota**: objekt přihlašovacích údajů implementující [ `System.Net.ICredentials` rozhraní](/dotnet/api/system.net.icredentials).
