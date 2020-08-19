---
ms.openlocfilehash: 9167b4b5943dd797c5a4cb20e53ee6832f0b3021
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623019"
---
1. <span data-ttu-id="b629a-101">Přejděte do složky, která obsahuje `.nupkg` soubor.</span><span class="sxs-lookup"><span data-stu-id="b629a-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="b629a-102">Spusťte následující příkaz, zadáním názvu balíčku (jedinečné ID balíčku) a nahrazením hodnoty klíče klíčem rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="b629a-102">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```dotnetcli
    dotnet nuget push AppLogger.1.0.0.nupkg --api-key qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 --source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="b629a-103">dotnet zobrazuje výsledky procesu publikování:</span><span class="sxs-lookup"><span data-stu-id="b629a-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="b629a-104">Podívejte se na téma [dotnet NuGet push](/dotnet/core/tools/dotnet-nuget-push).</span><span class="sxs-lookup"><span data-stu-id="b629a-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>