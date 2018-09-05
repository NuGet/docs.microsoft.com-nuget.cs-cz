---
title: Poskytovatelé přihlašovacích údajů nuget.exe
description: poskytovatelé přihlašovacích údajů nuget.exe ověřoval informační kanál a jsou implementovány jako spustitelné soubory příkazového řádku, které odpovídají konvencím konkrétní.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550186"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Ověřování informačních kanálů prostřednictvím nuget.exe poskytovatelé přihlašovacích údajů

*NuGet 3.3 +*

Když `nuget.exe` potřebuje přihlašovací údaje pro ověření pomocí informační kanál, pro ně vypadá takto:

1. NuGet nejprve hledá přihlašovací údaje v `Nuget.Config` soubory.
1. NuGet použije poskytovatelé modul plugin přihlašovacích údajů, v souladu s níže uvedeném pořadí. (A je příklad [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. NuGet potom zobrazí výzvu pro přihlašovací údaje na příkazovém řádku.

Všimněte si, že poskytovatelé přihlašovacích údajů je zde popsáno, fungovat pouze v `nuget.exe` a ne v "dotnet restore" nebo Visual Studio. Poskytovatelé přihlašovacích údajů pomocí sady Visual Studio, naleznete v tématu [nuget.exe poskytovatelé přihlašovacích údajů pro Visual Studio](nuget-credential-providers-for-visual-studio.md)

poskytovatelé přihlašovacích údajů nuget.exe dá 3 způsoby:

- **Globálně**: zpřístupnění poskytovatele přihlašovacích údajů pro všechny výskyty `nuget.exe` běžet pod aktuální uživatelského profilu, přidejte ji do `%LocalAppData%\NuGet\CredentialProviders`. Je potřeba vytvořit `CredentialProviders` složky. Poskytovatelé přihlašovacích údajů se dá nainstalovat na kořenovém adresáři `CredentialProviders` složku nebo podsložku. Pokud poskytovatel přihlašovacích údajů má více souborů nebo sestavení, můžete zachovat poskytovatelé uspořádané podsložky.

- **Z proměnné prostředí**: poskytovatelé přihlašovacích údajů mohou být uložena kdekoli a tak ho zpřístupnit `nuget.exe` nastavením `%NUGET_CREDENTIALPROVIDERS_PATH%` proměnnou prostředí pro umístění poskytovatele. Tato proměnná může být seznam oddělený středníkem (například `path1;path2`) Pokud máte víc umístění.

- **Vedle nuget.exe**: nuget.exe poskytovatelé přihlašovacích údajů mohou být umístěny ve stejné složce jako `nuget.exe`.

Při načítání poskytovatelé přihlašovacích údajů `nuget.exe` hledá výše uvedené umístění v pořadí, pro všechny soubory s názvem `credentialprovider*.exe`, pak načte těchto souborů v pořadí, se nenašel. Pokud ve stejné složce existuje více poskytovatelé přihlašovacích údajů, jsou načteny v abecedním pořadí.

## <a name="creating-a-nugetexe-credential-provider"></a>Vytvoření poskytovatele přihlašovacích údajů nuget.exe

Poskytovatel přihlašovacích údajů je spustitelného souboru příkazového řádku s názvem ve formě `CredentialProvider*.exe`, který shromažďuje vstupů, získá přihlašovací údaje podle potřeby a vrátí odpovídající ukončovací kód stavu a standardní výstup.

Zprostředkovatel musíte udělat toto:

- Určení, zda může poskytnout přihlašovací údaje pro cílový identifikátor URI před zahájením získání přihlašovacích údajů. Pokud ne, měla by vrátit stavový kód 1 bez pověření.
- Nelze změnit `Nuget.Config` (například nastavení přihlašovacích údajů existuje).
- Popisovač HTTP konfiguraci proxy serveru na svůj vlastní jako NuGet neposkytuje informace o proxy serveru pro modul plug-in.
- Vrátí přihlašovací údaje nebo podrobnosti o chybě `nuget.exe` zápisem objektu odpovědi JSON (viz níže) do stdout, pomocí kódování UTF-8.
- Volitelně vysílat protokolování další trasování do stderr. Žádné tajných kódů mají být někdy zapisovány do stderr, protože úrovni podrobností "normální" nebo "podrobné" Tato trasování opakována balíčkem NuGet do konzoly.
- Neočekávané parametry by měl být ignorovány, poskytuje kompatibilitu s budoucí verze balíčku nuget.

### <a name="input-parameters"></a>Vstupní parametry

| Parametr/přepínače |Popis|
|----------------|-----------|
| Identifikátor URI {value} | Identifikátor URI vyžadující přihlašovací údaje ke zdroji balíčku.|
| Neinteraktivní | Pokud jsou k dispozici, nevyvolá poskytovatele interaktivní výzvy. |
| isRetry | Pokud jsou k dispozici, určuje, že je tento pokus opakování dříve neúspěšném pokusu. Poskytovatelé obvykle používají tento příznak zajistíte, že všechny stávající mezipaměti obejít a výzvu pro nové přihlašovací údaje, pokud je to možné.|
| Úroveň podrobností {value} | Pokud jsou k dispozici, použijte některou z následujících hodnot: "normální", "quiet" nebo "podrobné". Pokud není zadána žádná hodnota, výchozí hodnota je "normální". Poskytovatelé by měl použít jako údaj o úroveň protokolování volitelné vygenerovat standardní chybový proud. |

### <a name="exit-codes"></a>Kódy ukončení

| Kód |Výsledek | Popis |
|----------------|-----------|-----------|
| 0 | Úspěch | Přihlašovací údaje byly úspěšně získány a byl zapsán do stdout.|
| 1 | ProviderNotApplicable | Aktuální zprostředkovatel neposkytuje přihlašovací údaje pro daný identifikátor URI.|
| 2 | selhání | Zprostředkovatel je správný zprostředkovatele pro daný identifikátor URI, ale nemůže poskytnout přihlašovací údaje. V takovém případě nuget.exe nebude opakovat pokus o ověření a se nezdaří. Typickým příkladem je, když uživatel zruší interaktivního přihlášení. |

### <a name="standard-output"></a>Standardní výstup

| Vlastnost |Poznámky|
|----------------|-----------|
| uživatelské jméno | Uživatelské jméno u ověřených požadavků.|
| Heslo | Heslo pro ověření žádosti.|
| Zpráva | Volitelné podrobnosti o odpověď, slouží pouze k zobrazení dalších podrobností v případy selhání. |

Příklad výstupu stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Řešení potíží s poskytovatele přihlašovacích údajů

V současné době nenabízí NuGet mnohem přímou podporu pro ladění poskytovatelé přihlašovacích údajů vlastní; [vydat 4598](https://github.com/NuGet/Home/issues/4598) sleduje tuto práci.

Můžete také provést následující:

- Spusťte nuget.exe s `-verbosity` přepínače ke kontrole podrobný výstup.
- Přidat zprávy ladění k `stdout` příslušných místech.
- Ujistěte se, že používáte nuget.exe 3.3 nebo novější.
- Připojte ladicí program při spuštění s tímto fragmentem kódu:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

O další pomoc [odeslat žádost o podporu nuget.org](https://www.nuget.org/policies/Contact).
