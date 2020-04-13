---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825163"
---
<span data-ttu-id="ee3dc-101">Použijte příkaz [dotnet restore,](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) který obnoví balíčky uvedené v souboru projektu (viz [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="ee3dc-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="ee3dc-102">S rozhraním .NET Core 2.0 a `dotnet build` `dotnet run`novějším se obnovení provádí automaticky pomocí rozhraní a .</span><span class="sxs-lookup"><span data-stu-id="ee3dc-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="ee3dc-103">Od NuGet 4.0, to spustí `nuget restore`stejný kód jako .</span><span class="sxs-lookup"><span data-stu-id="ee3dc-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="ee3dc-104">Stejně jako `dotnet` u ostatních příkazů rozhraní příkazového řádku nejprve otevřete příkazový řádek a přepněte do adresáře, který obsahuje soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="ee3dc-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="ee3dc-105">Obnovení balíčku pomocí `dotnet restore`:</span><span class="sxs-lookup"><span data-stu-id="ee3dc-105">To restore a package using `dotnet restore`:</span></span>

```dotnetcli
dotnet restore 
```