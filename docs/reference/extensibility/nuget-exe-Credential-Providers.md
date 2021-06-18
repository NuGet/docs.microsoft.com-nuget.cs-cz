---
title: nuget.exe zprostředkovatelů přihlašovacích údajů
description: nuget.exe přihlašovacích údajů ověřují pomocí informačního kanálu a jsou implementovány jako spustitelné soubory příkazového řádku, které dodržují konkrétní konvence.
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 4f0a5a2355b34c39a435d24691a3f8ea10ee9c00
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323827"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Ověřování informačních kanálů pomocí nuget.exe zprostředkovatelů přihlašovacích údajů

Ve verzi `3.3` byla přidána podpora pro `nuget.exe` konkrétní zprostředkovatele přihlašovacích údajů. Od té doby byla přidána `4.8` [podpora verzí pro zprostředkovatele](NuGet-Cross-Platform-Authentication-Plugin.md) přihlašovacích údajů, kteří pracují ve všech scénářích příkazového řádku ( `nuget.exe` , , `dotnet.exe` `msbuild.exe` ).

Další [podrobnosti o všech přístupech k](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) ověřování najdete v tématu Využívání balíčků z ověřených informačních kanálů. `nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>nuget.exe poskytovatele přihlašovacích údajů

nuget.exe přihlašovacích údajů je možné použít 3 způsoby:

- **Globálně:** Pokud chcete poskytovatele přihlašovacích údajů zprostředkovatele zprostředkovatele přihlašovacích údajů zprostředkovatele identity zprostředkovatele identity spustit v rámci profilu aktuálního uživatele, přidejte `nuget.exe` ho do `%LocalAppData%\NuGet\CredentialProviders` . Možná budete muset složku `CredentialProviders` vytvořit. Zprostředkovatele přihlašovacích údajů je možné nainstalovat v kořenovém adresáři `CredentialProviders`  složky nebo v podsložce. Pokud poskytovatel přihlašovacích údajů obsahuje více souborů nebo sestavení, můžete pomocí podsložek zachovat uspořádání poskytovatelů.

- **Z proměnné prostředí:** Poskytovatelé přihlašovacích údajů mohou být uloženi kdekoli a zpřístupněni nastavením proměnné prostředí `nuget.exe` na umístění `%NUGET_CREDENTIALPROVIDERS_PATH%` poskytovatele. Tato proměnná může být seznam oddělený středníkem (například ), pokud `path1;path2` máte více umístění.

- **Vedle nuget.exe**: nuget.exe zprostředkovatelé přihlašovacích údajů mohou být umístěny ve stejné složce jako `nuget.exe` .

Při načítání zprostředkovatelů přihlašovacích údajů vyhledá ve výše uvedených umístěních v uvedeném pořadí libovolný soubor s názvem a pak tyto soubory načte v pořadí, v uvedeném `nuget.exe` `credentialprovider*.exe` pořadí. Pokud ve stejné složce existuje více zprostředkovatelů přihlašovacích údajů, načítá se v abecedním pořadí.

## <a name="creating-a-nugetexe-credential-provider"></a>Vytvoření zprostředkovatele nuget.exe přihlašovacích údajů

Zprostředkovatel přihlašovacích údajů je spustitelný soubor příkazového řádku s názvem ve formátu , který shromažďuje vstupy, získává přihlašovací údaje podle potřeby a pak vrací odpovídající stavový kód ukončení a `CredentialProvider*.exe` standardní výstup.

Poskytovatel musí provést následující akce:

- Před zahájením získání přihlašovacích údajů zjistěte, jestli může poskytnout přihlašovací údaje pro cílový identifikátor URI. Pokud ne, měl by vrátit stavový kód 1 bez přihlašovacích údajů.
- `NuGet.Config`Neupravujte je (například nastavujte přihlašovací údaje).
- Konfigurace proxy serveru HTTP je sama o sobě, protože NuGet neposkytuje informace o proxy serveru modulu plug-in.
- Vraťte přihlašovací údaje nebo podrobnosti o chybě do souboru zápisem `nuget.exe` objektu odpovědi JSON (viz níže) do výstupu stdout pomocí kódování UTF-8.
- Volitelně můžete do stderr generovat další protokolování trasování. Do stderru by se nikdy neměly zapisovat žádné tajné kódy, protože nuGet na úrovni podrobností "normální" nebo "podrobné" takové trasování vyjádřuje NuGet do konzoly.
- Neočekávané parametry by se měly ignorovat a zajistit dopředné kompatibility s budoucími verzemi NuGetu.

### <a name="input-parameters"></a>Vstupní parametry

| Parametr/Přepínač |Description|
|----------------|-----------|
| Identifikátor URI {value} | Identifikátor URI zdroje balíčku, který vyžaduje přihlašovací údaje.|
| Neinteraktivní | Pokud je k dispozici, poskytovatel nevydá interaktivní výzvy. |
| IsRetry | Pokud je k dispozici, znamená to, že se jedná o pokus o opakování dříve neúspěšných pokusů. Poskytovatelé obvykle tento příznak používají k tomu, aby zajistili, že obejití existující mezipaměti, a pokud je to možné, zobrazí se výzva k zadání nových přihlašovacích údajů.|
| Podrobnost {value} | Pokud je k dispozici, jedna z následujících hodnot: "normal", "quiet" nebo "detailed". Pokud není zadána žádná hodnota, výchozí hodnota je "normální". Poskytovatelé by měli tuto úroveň použít jako indikaci úrovně volitelného protokolování pro vysílání do standardního chybového streamu. |

### <a name="exit-codes"></a>Ukončovací kódy

| Kód |Výsledek | Popis |
|----------------|-----------|-----------|
| 0 | Success | Přihlašovací údaje se úspěšně získaly a byly zapsány do stdout.|
| 1 | PoskytovatelNotApplicable | Aktuální zprostředkovatel neposkytuje přihlašovací údaje pro daný identifikátor URI.|
| 2 | Selhání | Zprostředkovatel je správným zprostředkovatelem pro daný identifikátor URI, ale nemůže zadat přihlašovací údaje. V takovém případě nuget.exe nebude opakovat ověřování a selže. Typickým příkladem je zrušení interaktivního přihlášení uživatelem. |

### <a name="standard-output"></a>Standardní výstup

| Vlastnost |Poznámky|
|----------------|-----------|
| Uživatelské jméno | Uživatelské jméno pro ověřené požadavky.|
| Heslo | Heslo pro ověřené požadavky.|
| Zpráva | Volitelné podrobnosti o odpovědi, které slouží pouze k zobrazení dalších podrobností v případech selhání. |

Příklad stdout:

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a>Řešení potíží s poskytovatelem přihlašovacích údajů

NuGet v současné době neposkytuje přímou podporu ladění vlastních zprostředkovatelů přihlašovacích údajů. [problém 4598](https://github.com/NuGet/Home/issues/4598) tuto práci sleduje.

Můžete také provést následující:

- Spusťte nuget.exe `-verbosity` přepínačem a zkontrolujte podrobný výstup.
- Na příslušných místech `stdout` přidejte do souboru ladicí zprávy.
- Ujistěte se, že používáte nuget.exe 3.3 nebo vyšší.
- Připojte ladicí program při spuštění pomocí tohoto fragmentu kódu:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
