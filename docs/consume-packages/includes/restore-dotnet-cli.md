---
ms.openlocfilehash: 9764479d88cc8d87a9f455e64bd46ae8de15055d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860604"
---
<span data-ttu-id="ee0e5-101">Použijte příkaz [dotnet Restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) , který obnoví balíčky uvedené v souboru projektu (viz [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="ee0e5-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="ee0e5-102">Pomocí .NET Core 2,0 a novějšího se obnovení provádí automaticky s `dotnet build` a `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="ee0e5-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="ee0e5-103">Od NuGet 4,0 to spustí stejný kód jako `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="ee0e5-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="ee0e5-104">Stejně jako u ostatních `dotnet` příkazů CLI otevřete příkazový řádek a přejděte do adresáře, který obsahuje soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="ee0e5-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="ee0e5-105">Postup obnovení balíčku pomocí `dotnet restore`:</span><span class="sxs-lookup"><span data-stu-id="ee0e5-105">To restore a package using `dotnet restore`:</span></span>

```cli
dotnet restore 
```