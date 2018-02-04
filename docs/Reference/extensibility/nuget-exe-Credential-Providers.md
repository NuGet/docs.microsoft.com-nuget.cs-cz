---
title: "Poskytovatelé přihlašovacích údajů nuget.exe | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "poskytovatelé přihlašovacích údajů nuget.exe ověření prostřednictvím informačního kanálu a jsou implementované jako příkazového řádku spustitelné soubory, které dodržují konvence konkrétní prostředí."
keywords: "poskytovatelé přihlašovacích údajů nuget.exe, poskytovatel pověření rozhraní API, ověřování pomocí informačního kanálu, ověřování pomocí Galerie"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88ce0106ad4e628ba8120f94b7951c7746ab67f3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Ověřování informačních kanálů s nuget.exe poskytovatelé přihlašovacích údajů

*NuGet 3.3 +*

Když `nuget.exe` potřebuje přihlašovací údaje k ověřování pro informační kanál, vypadá pro ně následujícím způsobem:

1. NuGet nejprve hledá přihlašovací údaje v `Nuget.Config` soubory.
1. NuGet pak použije poskytovatelé přihlašovacích údajů modul plug-in, podstoupí níže uvedeném pořadí. (A je třeba [Visual Studio Team Services přihlašovací údaje poskytovatele](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. NuGet vyzve uživatele k zadání přihlašovacích údajů na příkazovém řádku.

Všimněte si, že poskytovatelé přihlašovacích údajů, které jsou zde popsané fungovat pouze v `nuget.exe` a není v 'dotnet obnovení, nebo Visual Studio. Poskytovatelé přihlašovacích údajů pomocí sady Visual Studio, najdete v části [nuget.exe poskytovatelé přihlašovacích údajů pro sadu Visual Studio](nuget-credential-providers-for-visual-studio.md)

poskytovatelé přihlašovacích údajů nuget.exe mohou být používány 3 způsoby:

- **Globálně**: Chcete-li k dispozici pro všechny instance poskytovatele přihlašovacích údajů `nuget.exe` běžet pod aktuální uživatelský profil, přidejte ho do `%LocalAppData%\NuGet\CredentialProviders`. Budete muset vytvořit `CredentialProviders` složky. Poskytovatelé přihlašovacích údajů se dá nainstalovat na kořenovém `CredentialProviders` složku nebo podsložku. Pokud poskytovatel pověření má několik souborů nebo sestavení, můžete zachovat zprostředkovatele uspořádané podsložky.

- **Na proměnné prostředí**: poskytovatelé přihlašovacích údajů můžete uložit kdekoli a přístupné `nuget.exe` nastavením `%NUGET_CREDENTIALPROVIDERS_PATH%` proměnnou prostředí k umístění poskytovatele. Tato proměnná může být seznam oddělených středníkem (například `path1;path2`) Pokud máte více lokalit.

- **Spolu s nuget.exe**: nuget.exe poskytovatelé přihlašovacích údajů mohou být umístěny ve stejné složce jako `nuget.exe`.

Při načítání poskytovatelé přihlašovacích údajů, `nuget.exe` hledá výše uvedené umístění, aby všechny soubory s názvem `credentialprovider*.exe`, potom se načte těchto souborů v pořadí, které se nacházejí. Pokud existuje více poskytovatelů pověření ve stejné složce, jsou načíst v abecedním pořadí.

## <a name="creating-a-nugetexe-credential-provider"></a>Vytvoření zprostředkovatele nuget.exe přihlašovacích údajů

Poskytovatel pověření je spustitelného souboru příkazového řádku, s názvem ve formátu `CredentialProvider*.exe`, který shromažďuje vstupy, získá přihlašovací údaje podle potřeby a vrátí ukončovací odpovídající stavový kód a standardní výstup.

Zprostředkovatel postupujte takto:

- Určí, zda může poskytnout přihlašovací údaje pro cílový identifikátor URI před zahájením získání přihlašovacích údajů. Pokud ne, měla by vrátit stavovým kódem 1 bez pověření.
- Nelze změnit `Nuget.Config` (například nastavení přihlašovacích údajů existuje).
- Popisovač HTTP konfiguraci proxy serveru na svůj vlastní jako NuGet neposkytuje informace o proxy serveru pro tento modul plug-in.
- Vrátí přihlašovací údaje nebo podrobnosti o chybě `nuget.exe` zápisem objekt odpovědi JSON (viz níže) do datového proudu stdout pomocí kódování UTF-8.
- Volitelně emitování protokolování další trasování do stderr. Žádné tajné klíče někdy budou zasílány do stderr, protože úrovni podrobností "normální" nebo "podrobné" takové trasování opakována rozšířením NuGet do konzoly.
- Neočekávané parametry by měl být ignorovány, poskytuje dopřednou kompatibilitu s budoucími verzemi NuGet.

### <a name="input-parameters"></a>Vstupní parametry

| Parametr/přepínače |Popis|
|----------------|-----------|
| Identifikátor URI {value} | Identifikátor URI vyžadují přihlašovací údaje ke zdroji balíčku.|
| Neinteraktivní | Pokud je k dispozici, zprostředkovatele nevydává interaktivní výzvy. |
| IsRetry | Pokud je k dispozici, označuje, že je tento pokus dříve neúspěšných pokusů o opakování. Poskytovatelé obvykle používají tento příznak k zajistěte, aby vynechat všechny existující mezipaměti a výzvu k nové přihlašovací údaje, pokud je to možné.|
| Podrobností {value} | Pokud je k dispozici, jednu z následujících hodnot: "normální", "quiet" nebo "podrobné". Pokud je zadána žádná hodnota, použije výchozí hodnota "normální". Zprostředkovatelé by měl použít jako údajem o úroveň protokolování volitelné pro vydávání na standardní chybový proud. |

### <a name="exit-codes"></a>Kódy ukončení

| Kód |Výsledek | Popis |
|----------------|-----------|-----------|
| 0 | Úspěch | Přihlašovací údaje úspěšně získala a byl zapsán do stdout.|
| 1 | ProviderNotApplicable | Aktuální zprostředkovatel neposkytuje přihlašovací údaje pro daný identifikátor URI.|
| 2 | Selhání | Zprostředkovatel je správný zprostředkovatele pro daný identifikátor URI, ale nelze poskytnout pověření. V takovém případě nuget.exe nebude opakovat pokus o ověření a se nezdaří. Typickým příkladem je, když uživatel zruší interaktivní přihlášení. |

### <a name="standard-output"></a>Standardní výstup

| Vlastnost |Poznámky|
|----------------|-----------|
| Uživatelské jméno | Uživatelské jméno u ověřených požadavků.|
| Heslo | Heslo pro ověření žádosti.|
| Zpráva | Volitelné údaje o odpověď, používají pouze pro účely zobrazit další podrobnosti v případě selhání. |

Příklad stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Řešení potíží s poskytovatel pověření

V současné době NuGet neposkytuje mnohem přímé podpory pro ladění zprostředkovatelů vlastní pověření; [vydání 4598](https://github.com/NuGet/Home/issues/4598) je sledování této práce.

Můžete provést také následující:

- Spustit nuget.exe s `-verbosity` přepínač tak, aby kontrolovat podrobný výstup.
- Přidat zprávy ladění na `stdout` příslušná místa.
- Ujistěte se, že používáte nuget.exe 3.3 nebo vyšší.
- Připojte ladicí program při spuštění s Tento fragment kódu:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

Další informace [odeslat žádost o podporu nuget.org](https://www.nuget.org/policies/Contact).
