---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860588"
---
Použijte příkaz [Restore](../../reference/cli-reference/cli-ref-restore.md) , který stáhne a nainstaluje ze složky Packages chybějící balíčky.

Pro projekty migrované do PackageReference použijte místo toho nástroj [MSBuild-t:Restore](../package-restore.md#restore-using-msbuild) k obnovení balíčků.

`restore`přidá pouze balíčky na disk, ale nemění závislosti projektu. Chcete-li obnovit závislosti projektu `packages.config`, upravte a pak `restore` použijte příkaz.

Stejně jako u ostatních `nuget.exe` příkazů CLI otevřete příkazový řádek a přejděte do adresáře, který obsahuje soubor projektu.

Postup obnovení balíčku pomocí `restore`:

```cli
nuget restore MySolution.sln
```