---
title: Poskytovatelé přihlašovacích údajů NuGet. exe
description: Zprostředkovatelé pověření NuGet. exe ověřují pomocí informačního kanálu a jsou implementováni jako spustitelné soubory příkazového řádku, které následují konkrétní konvence.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230782"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Ověřování informačních kanálů pomocí zprostředkovatelů pověření NuGet. exe

Ve verzi `3.3` byla přidána podpora pro `nuget.exe` zprostředkovatelům přihlašovacích údajů. Od té doby se v nástroji verze `4.8` [Podpora zprostředkovatelů přihlašovacích údajů](NuGet-Cross-Platform-Authentication-Plugin.md) , které fungují ve všech scénářích příkazového řádku (`nuget.exe`, `dotnet.exe`, `msbuild.exe`).

Další podrobnosti o všech přístupech k ověřování pro `nuget.exe` najdete v tématu [využívání balíčků ze ověřených informačních kanálů](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) .

## <a name="nugetexe-credential-provider-discovery"></a>zjišťování poskytovatele přihlašovacích údajů NuGet. exe

poskytovatelé přihlašovacích údajů NuGet. exe se dají použít třemi způsoby:

- **Globálně**: Pokud chcete poskytovatele přihlašovacích údajů zpřístupnit všem instancím `nuget.exe` běžet pod profilem aktuálního uživatele, přidejte ho do `%LocalAppData%\NuGet\CredentialProviders`. Možná budete muset vytvořit složku `CredentialProviders`. Poskytovatelé přihlašovacích údajů se dají nainstalovat do kořenového adresáře `CredentialProviders` složky nebo do podsložky. Pokud má poskytovatel přihlašovacích údajů více souborů nebo sestavení, můžete použít podsložky a zachovat tak jejich poskytovatele.

- **Z proměnné prostředí**: poskytovatelé přihlašovacích údajů můžou být uložené kdekoli a zpřístupnit pro `nuget.exe` nastavením proměnné prostředí `%NUGET_CREDENTIALPROVIDERS_PATH%` na umístění poskytovatele. Tato proměnná může být seznam oddělený středníkem (například `path1;path2`), pokud máte více umístění.

- **Společně se NuGet. exe**: poskytovatelé přihlašovacích údajů NuGet. exe se dají umístit do stejné složky jako `nuget.exe`.

Při načítání zprostředkovatelů přihlašovacích údajů `nuget.exe` vyhledá v případě libovolného souboru s názvem `credentialprovider*.exe`tato umístění v pořadí, ve kterém se budou soubory nacházet. Pokud ve stejné složce existuje více zprostředkovatelů přihlašovacích údajů, načtou se v abecedním pořadí.

## <a name="creating-a-nugetexe-credential-provider"></a>Vytvoření poskytovatele pověření NuGet. exe

Poskytovatel pověření je spustitelný soubor příkazového řádku s názvem ve formě `CredentialProvider*.exe`, který shromáždí vstupy, získá pověření podle potřeby a vrátí odpovídající stavový kód ukončení a standardní výstup.

Poskytovatel musí provádět tyto akce:

- Před zahájením získání přihlašovacích údajů určete, jestli může poskytnout přihlašovací údaje pro cílový identifikátor URI. V takovém případě by měl vrátit stavový kód 1 bez přihlašovacích údajů.
- Neupravujte `Nuget.Config` (například nastavení přihlašovacích údajů).
- Vlastní zpracování konfigurace proxy HTTP, protože NuGet neposkytuje informace o proxy serveru modulu plug-in.
- Vraťte přihlašovací údaje nebo podrobnosti chyby k `nuget.exe` zápisem objektu odpovědi JSON (viz níže) do STDOUT pomocí kódování UTF-8.
- Volitelně můžete vygenerovat další protokolování trasování do stderr. Do stderr by se nikdy neměly zapisovat žádná tajná klíčová slova, protože u úrovní podrobností "normální" nebo "podrobná" jsou trasování v rámci nástroje NuGet pro konzolu odezva.
- Neočekávané parametry by měly být ignorovány, čímž je zajištěna dopředná kompatibilita s budoucími verzemi NuGet.

### <a name="input-parameters"></a>Vstupní parametry

| Parametr/Switch |Popis|
|----------------|-----------|
| Identifikátor URI {Value} | Identifikátor URI zdroje balíčku vyžaduje přihlašovací údaje.|
| NonInteractive | Pokud je přítomen, zprostředkovatel nevydá interaktivní výzvy. |
| Opakování | Pokud je k dispozici, znamená to, že se tento pokus pokusí o opakování dříve neúspěšného pokusu. Poskytovatelé obvykle používají tento příznak k zajištění toho, aby využívali jakoukoli existující mezipaměť a zobrazila výzvu k zadání nových přihlašovacích údajů|
| Podrobnosti {Value} | Pokud je k dispozici jedna z následujících hodnot: "normální", "tichá" nebo "podrobná". Pokud není zadaná žádná hodnota, použije se výchozí hodnota "Normal". Poskytovatelé by ho měli používat jako indikaci úrovně volitelného protokolování, které se má vygenerovat do standardního chybového proudu. |

### <a name="exit-codes"></a>Ukončovací kódy

| Kód |Výsledek | Popis |
|----------------|-----------|-----------|
| 0 | Úspěch | Přihlašovací údaje byly úspěšně získány a zapsány do STDOUT.|
| 1 | ProviderNotApplicable | Aktuální zprostředkovatel neposkytuje přihlašovací údaje pro daný identifikátor URI.|
| 2 | Nezdařilo se | Zprostředkovatel je správného poskytovatele pro daný identifikátor URI, ale nemůže poskytnout přihlašovací údaje. V takovém případě NuGet. exe nebude opakovat ověřování a selže. Typickým příkladem je, že uživatel zruší interaktivní přihlášení. |

### <a name="standard-output"></a>Standardní výstup

| Vlastnost |Poznámky:|
|----------------|-----------|
| Uživatelské jméno | Uživatelské jméno pro ověřené požadavky.|
| Heslo | Heslo pro ověřené požadavky.|
| Zpráva | Volitelné podrobnosti o odpovědi, které se používají jenom k zobrazení dalších podrobností v případech selhání. |

Příklad stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Řešení potíží s poskytovatelem přihlašovacích údajů

V současné době NuGet neposkytuje mnohem přímou podporu pro ladění vlastních poskytovatelů přihlašovacích údajů; Tato práce sleduje [problém 4598](https://github.com/NuGet/Home/issues/4598) .

Můžete také provést následující akce:

- Spuštěním nástroje NuGet. exe s přepínačem `-verbosity` zkontrolujte podrobný výstup.
- Přidejte zprávy pro ladění `stdout` na vhodných místech.
- Ujistěte se, že používáte NuGet. exe 3,3 nebo vyšší.
- Připojit ladicí program při spuštění pomocí tohoto fragmentu kódu:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
