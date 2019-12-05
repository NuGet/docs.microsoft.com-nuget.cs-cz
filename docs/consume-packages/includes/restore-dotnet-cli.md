---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825163"
---
<span data-ttu-id="5c573-101">Použijte příkaz [dotnet Restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) , který obnoví balíčky uvedené v souboru projektu (viz [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="5c573-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="5c573-102">Pomocí .NET Core 2,0 a novějšího se obnovení provádí automaticky pomocí `dotnet build` a `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="5c573-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="5c573-103">Od NuGet 4,0 to spustí stejný kód jako `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="5c573-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="5c573-104">Stejně jako u ostatních příkazů rozhraní příkazového řádku (CLI) `dotnet` otevřete příkazový řádek a přejděte do adresáře, který obsahuje soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="5c573-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="5c573-105">Postup obnovení balíčku pomocí `dotnet restore`:</span><span class="sxs-lookup"><span data-stu-id="5c573-105">To restore a package using `dotnet restore`:</span></span>

```dotnetcli
dotnet restore 
```