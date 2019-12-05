---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825163"
---
Použijte příkaz [dotnet Restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) , který obnoví balíčky uvedené v souboru projektu (viz [PackageReference](../../consume-packages/package-references-in-project-files.md)). Pomocí .NET Core 2,0 a novějšího se obnovení provádí automaticky pomocí `dotnet build` a `dotnet run`. Od NuGet 4,0 to spustí stejný kód jako `nuget restore`.

Stejně jako u ostatních příkazů rozhraní příkazového řádku (CLI) `dotnet` otevřete příkazový řádek a přejděte do adresáře, který obsahuje soubor projektu.

Postup obnovení balíčku pomocí `dotnet restore`:

```dotnetcli
dotnet restore 
```