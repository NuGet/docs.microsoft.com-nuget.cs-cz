---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495961"
---
<span data-ttu-id="c1eee-101">Chyby `push` z příkazu obvykle označují problém.</span><span class="sxs-lookup"><span data-stu-id="c1eee-101">Errors from the `push` command typically indicate the problem.</span></span> <span data-ttu-id="c1eee-102">Je například možné, že jste zapomněli aktualizovat číslo verze v projektu a proto se pokoušíte publikovat balíček, který již existuje.</span><span class="sxs-lookup"><span data-stu-id="c1eee-102">For example, you may have forgotten to update the version number in your project and are therefore trying to publish a package that already exists.</span></span>

<span data-ttu-id="c1eee-103">Zobrazí se také chyby při pokusu o publikování balíčku pomocí identifikátoru, který již na hostiteli existuje.</span><span class="sxs-lookup"><span data-stu-id="c1eee-103">You also see errors when trying to publish a package using an identifier that already exists on the host.</span></span> <span data-ttu-id="c1eee-104">Název "AppLogger", například, již existuje.</span><span class="sxs-lookup"><span data-stu-id="c1eee-104">The name "AppLogger", for example, already exists.</span></span> <span data-ttu-id="c1eee-105">V takovém případě `push` příkaz udává následující chybu:</span><span class="sxs-lookup"><span data-stu-id="c1eee-105">In such a case, the `push` command gives the following error:</span></span>

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

<span data-ttu-id="c1eee-106">Pokud používáte platný klíč rozhraní API, který jste právě vytvořili, pak tato zpráva označuje konflikt názvů, který není zcela jasné z "oprávnění" část chyby.</span><span class="sxs-lookup"><span data-stu-id="c1eee-106">If you're using a valid API key that you just created, then this message indicates a naming conflict, which isn't entirely clear from the "permission" part of the error.</span></span> <span data-ttu-id="c1eee-107">Změňte identifikátor balíčku, znovu vytvořte `.nupkg` projekt, znovu `push` vytvořte soubor a opakujte příkaz.</span><span class="sxs-lookup"><span data-stu-id="c1eee-107">Change the package identifier, rebuild the project, recreate the `.nupkg` file, and retry the `push` command.</span></span>