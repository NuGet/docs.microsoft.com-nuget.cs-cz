---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860588"
---
<span data-ttu-id="aa242-101">Použijte příkaz [Restore](../../reference/cli-reference/cli-ref-restore.md) , který stáhne a nainstaluje ze složky Packages chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="aa242-101">Use the [restore](../../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="aa242-102">Pro projekty migrované do PackageReference použijte místo toho nástroj [MSBuild-t:Restore](../package-restore.md#restore-using-msbuild) k obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="aa242-102">For projects migrated to PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) to restore packages instead.</span></span>

<span data-ttu-id="aa242-103">`restore`přidá pouze balíčky na disk, ale nemění závislosti projektu.</span><span class="sxs-lookup"><span data-stu-id="aa242-103">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="aa242-104">Chcete-li obnovit závislosti projektu `packages.config`, upravte a pak `restore` použijte příkaz.</span><span class="sxs-lookup"><span data-stu-id="aa242-104">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="aa242-105">Stejně jako u ostatních `nuget.exe` příkazů CLI otevřete příkazový řádek a přejděte do adresáře, který obsahuje soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="aa242-105">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="aa242-106">Postup obnovení balíčku pomocí `restore`:</span><span class="sxs-lookup"><span data-stu-id="aa242-106">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```