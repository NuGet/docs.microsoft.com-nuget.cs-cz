---
title: Poskytovatelé přihlašovacích údajů nuget.exe
description: nuget.exe poskytovatelé přihlašovacích údajů ověřují pomocí informačního kanálu a jsou implementovány jako spustitelné soubory příkazového řádku, které následují konkrétní konvence.
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 285504508fa88c96f5c7a23f15ef14d81ebc21e1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777763"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Ověřování informačních kanálů s nuget.exe zprostředkovateli přihlašovacích údajů

V `3.3` podpoře verze se přidaly pro `nuget.exe` konkrétní poskytovatele přihlašovacích údajů. Od té doby byla v `4.8` [podpoře verzí pro poskytovatele přihlašovacích údajů](NuGet-Cross-Platform-Authentication-Plugin.md) , které fungují ve všech scénářích příkazového řádku ( `nuget.exe` , `dotnet.exe` , `msbuild.exe` ), přidána.

Další podrobnosti o všech přístupech k ověřování pro najdete v tématu [využívání balíčků ze ověřených informačních kanálů](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) . `nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>Zjišťování poskytovatele pověření nuget.exe

Poskytovatelé přihlašovacích údajů nuget.exe můžou používat 3 způsoby:

- **Globálně**: Pokud chcete poskytovatele přihlašovacích údajů zpřístupnit všem instancím `nuget.exe` běhu v profilu aktuálního uživatele, přidejte ho do `%LocalAppData%\NuGet\CredentialProviders` . Možná budete muset vytvořit `CredentialProviders` složku. Poskytovatelé přihlašovacích údajů se dají nainstalovat do kořenového adresáře `CredentialProviders`  složky nebo do podsložky. Pokud má poskytovatel přihlašovacích údajů více souborů nebo sestavení, můžete použít podsložky a zachovat tak jejich poskytovatele.

- **Z proměnné prostředí**: poskytovatelé přihlašovacích údajů můžou být uložené kdekoli a zpřístupněni tak, že `nuget.exe` nastaví `%NUGET_CREDENTIALPROVIDERS_PATH%` proměnnou prostředí na umístění poskytovatele. Tato proměnná může být seznam oddělený středníkem (například), `path1;path2` Pokud máte více umístění.

- **Vedle nuget.exe**: poskytovatelé přihlašovacích údajů nuget.exe můžou umístit do stejné složky jako `nuget.exe` .

Při načítání zprostředkovatelů přihlašovacích údajů `nuget.exe` prohledají výše uvedená umístění v případě libovolného souboru s názvem `credentialprovider*.exe` a pak tyto soubory načte v pořadí, v jakém byly nalezeny. Pokud ve stejné složce existuje více zprostředkovatelů přihlašovacích údajů, načtou se v abecedním pořadí.

## <a name="creating-a-nugetexe-credential-provider"></a>Vytvoření poskytovatele pověření nuget.exe

Poskytovatel pověření je spustitelný soubor příkazového řádku pojmenovaný ve formuláři `CredentialProvider*.exe` , který shromáždí vstupy, získá přihlašovací údaje podle potřeby a vrátí příslušný stavový kód ukončení a standardní výstup.

Poskytovatel musí provádět tyto akce:

- Před zahájením získání přihlašovacích údajů určete, jestli může poskytnout přihlašovací údaje pro cílový identifikátor URI. V takovém případě by měl vrátit stavový kód 1 bez přihlašovacích údajů.
- Neupravovat `Nuget.Config` (jako je třeba nastavení přihlašovacích údajů).
- Vlastní zpracování konfigurace proxy HTTP, protože NuGet neposkytuje informace o proxy serveru modulu plug-in.
- Vraťte přihlašovací údaje nebo podrobnosti chyby do `nuget.exe` zápisu objektu odpovědi JSON (viz níže) do STDOUT pomocí kódování UTF-8.
- Volitelně můžete vygenerovat další protokolování trasování do stderr. Do stderr by se nikdy neměly zapisovat žádná tajná klíčová slova, protože u úrovní podrobností "normální" nebo "podrobná" jsou trasování v rámci nástroje NuGet pro konzolu odezva.
- Neočekávané parametry by měly být ignorovány, čímž je zajištěna dopředná kompatibilita s budoucími verzemi NuGet.

### <a name="input-parameters"></a>Vstupní parametry

| Parametr/Switch |Popis|
|----------------|-----------|
| Identifikátor URI {Value} | Identifikátor URI zdroje balíčku vyžaduje přihlašovací údaje.|
| Neinteraktivní | Pokud je přítomen, zprostředkovatel nevydá interaktivní výzvy. |
| Opakování | Pokud je k dispozici, znamená to, že se tento pokus pokusí o opakování dříve neúspěšného pokusu. Poskytovatelé obvykle používají tento příznak k zajištění toho, aby využívali jakoukoli existující mezipaměť a zobrazila výzvu k zadání nových přihlašovacích údajů|
| Podrobnosti {Value} | Pokud je k dispozici jedna z následujících hodnot: "normální", "tichá" nebo "podrobná". Pokud není zadaná žádná hodnota, použije se výchozí hodnota "Normal". Poskytovatelé by ho měli používat jako indikaci úrovně volitelného protokolování, které se má vygenerovat do standardního chybového proudu. |

### <a name="exit-codes"></a>Ukončovací kódy

| Kód |Výsledek | Popis |
|----------------|-----------|-----------|
| 0 | Success | Přihlašovací údaje byly úspěšně získány a zapsány do STDOUT.|
| 1 | ProviderNotApplicable | Aktuální zprostředkovatel neposkytuje přihlašovací údaje pro daný identifikátor URI.|
| 2 | Selhání | Zprostředkovatel je správného poskytovatele pro daný identifikátor URI, ale nemůže poskytnout přihlašovací údaje. V takovém případě se nuget.exe neopakuje ověřování a nezdaří se. Typickým příkladem je, že uživatel zruší interaktivní přihlášení. |

### <a name="standard-output"></a>Standardní výstup

| Vlastnost |Poznámky|
|----------------|-----------|
| Uživatelské jméno | Uživatelské jméno pro ověřené požadavky.|
| Heslo | Heslo pro ověřené požadavky.|
| Zpráva | Volitelné podrobnosti o odpovědi, které se používají jenom k zobrazení dalších podrobností v případech selhání. |

Příklad stdout:

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a>Řešení potíží s poskytovatelem přihlašovacích údajů

V současné době NuGet neposkytuje mnohem přímou podporu pro ladění vlastních poskytovatelů přihlašovacích údajů; Tato práce sleduje [problém 4598](https://github.com/NuGet/Home/issues/4598) .

Můžete také provést následující:

- Spusťte nuget.exe s `-verbosity` přepínačem pro kontrolu podrobného výstupu.
- Na vhodné místo přidejte zprávy pro ladění `stdout` .
- Ujistěte se, že používáte nuget.exe 3,3 nebo vyšší.
- Připojit ladicí program při spuštění pomocí tohoto fragmentu kódu:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
