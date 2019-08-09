---
ms.openlocfilehash: 9764479d88cc8d87a9f455e64bd46ae8de15055d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860604"
---
Použijte příkaz [dotnet Restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) , který obnoví balíčky uvedené v souboru projektu (viz [PackageReference](../../consume-packages/package-references-in-project-files.md)). Pomocí .NET Core 2,0 a novějšího se obnovení provádí automaticky s `dotnet build` a `dotnet run`. Od NuGet 4,0 to spustí stejný kód jako `nuget restore`.

Stejně jako u ostatních `dotnet` příkazů CLI otevřete příkazový řádek a přejděte do adresáře, který obsahuje soubor projektu.

Postup obnovení balíčku pomocí `dotnet restore`:

```cli
dotnet restore 
```