---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860588"
---
Použijte příkaz [obnovit,](../../reference/cli-reference/cli-ref-restore.md) který stáhne a nainstaluje všechny balíčky, které ve složce *balíčky* chybí.

Pro projekty migrované na PackageReference použijte [msbuild -t:restore](../package-restore.md#restore-using-msbuild) k obnovení balíčků.

`restore`pouze přidává balíčky na disk, ale nezmění závislosti projektu. Chcete-li obnovit závislosti `packages.config`projektu, `restore` upravte a použijte příkaz.

Stejně jako `nuget.exe` u ostatních příkazů rozhraní příkazového řádku nejprve otevřete příkazový řádek a přepněte do adresáře, který obsahuje soubor projektu.

Obnovení balíčku pomocí `restore`:

```cli
nuget restore MySolution.sln
```