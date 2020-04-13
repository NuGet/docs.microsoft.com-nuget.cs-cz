---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860588"
---
<span data-ttu-id="68ebc-101">Použijte příkaz [obnovit,](../../reference/cli-reference/cli-ref-restore.md) který stáhne a nainstaluje všechny balíčky, které ve složce *balíčky* chybí.</span><span class="sxs-lookup"><span data-stu-id="68ebc-101">Use the [restore](../../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="68ebc-102">Pro projekty migrované na PackageReference použijte [msbuild -t:restore](../package-restore.md#restore-using-msbuild) k obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="68ebc-102">For projects migrated to PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) to restore packages instead.</span></span>

<span data-ttu-id="68ebc-103">`restore`pouze přidává balíčky na disk, ale nezmění závislosti projektu.</span><span class="sxs-lookup"><span data-stu-id="68ebc-103">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="68ebc-104">Chcete-li obnovit závislosti `packages.config`projektu, `restore` upravte a použijte příkaz.</span><span class="sxs-lookup"><span data-stu-id="68ebc-104">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="68ebc-105">Stejně jako `nuget.exe` u ostatních příkazů rozhraní příkazového řádku nejprve otevřete příkazový řádek a přepněte do adresáře, který obsahuje soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="68ebc-105">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="68ebc-106">Obnovení balíčku pomocí `restore`:</span><span class="sxs-lookup"><span data-stu-id="68ebc-106">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```