---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495961"
---
Chyby `push` z příkazu obvykle označují problém. Je například možné, že jste zapomněli aktualizovat číslo verze v projektu a proto se pokoušíte publikovat balíček, který již existuje.

Zobrazí se také chyby při pokusu o publikování balíčku pomocí identifikátoru, který již na hostiteli existuje. Název "AppLogger", například, již existuje. V takovém případě `push` příkaz udává následující chybu:

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

Pokud používáte platný klíč rozhraní API, který jste právě vytvořili, pak tato zpráva označuje konflikt názvů, který není zcela jasné z "oprávnění" část chyby. Změňte identifikátor balíčku, znovu vytvořte `.nupkg` projekt, znovu `push` vytvořte soubor a opakujte příkaz.