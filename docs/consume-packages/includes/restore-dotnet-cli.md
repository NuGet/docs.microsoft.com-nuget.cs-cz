---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825163"
---
Použijte příkaz [dotnet restore,](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) který obnoví balíčky uvedené v souboru projektu (viz [PackageReference](../../consume-packages/package-references-in-project-files.md)). S rozhraním .NET Core 2.0 a `dotnet build` `dotnet run`novějším se obnovení provádí automaticky pomocí rozhraní a . Od NuGet 4.0, to spustí `nuget restore`stejný kód jako .

Stejně jako `dotnet` u ostatních příkazů rozhraní příkazového řádku nejprve otevřete příkazový řádek a přepněte do adresáře, který obsahuje soubor projektu.

Obnovení balíčku pomocí `dotnet restore`:

```dotnetcli
dotnet restore 
```