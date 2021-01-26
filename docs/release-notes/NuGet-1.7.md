---
title: Zpráva k vydání verze NuGet 1,7
description: Poznámky k verzi pro NuGet 1,7, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777061"
---
# <a name="nuget-17-release-notes"></a>Zpráva k vydání verze NuGet 1,7

Zpráva k [vydání verze](../release-notes/nuget-1.6.md)  |  NuGet 1,6 Zpráva k [vydání verze NuGet 1,8](../release-notes/nuget-1.8.md)

NuGet 1,7 byl vydán 4. dubna 2012.

## <a name="known-installation-issue"></a>Známý problém s instalací
Pokud používáte VS 2010 SP1, můžete při pokusu o upgrade NuGetu v případě, že máte nainstalovanou starší verzi, spustit chybu instalace.

Alternativním řešením je jednoduše odinstalovat NuGet a pak ji nainstalovat z galerie rozšíření VS.  Další informace naleznete v tématu <https://support.microsoft.com/kb/2581019>.

Poznámka: Pokud Visual Studio neumožní odinstalovat rozšíření (tlačítko Odinstalace je zakázané), pak budete pravděpodobně muset restartovat Visual Studio pomocí možnosti Spustit jako správce.

## <a name="features"></a>Funkce

### <a name="support-opening-readmetxt-file-after-installation"></a>Podpora otevírání souboru readme.txt po instalaci
Novinka v 1,7, pokud balíček obsahuje `readme.txt` soubor v kořenu balíčku, NuGet po dokončení instalace balíčku automaticky otevře tento soubor.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Zobrazit předběžné verze balíčků v dialogovém okně Spravovat balíčky NuGet
Dialog spravovat balíčky NuGet teď obsahuje rozevírací seznam, který nabízí možnost zobrazovat předběžné verze balíčků.

![Zobrazení předprodejních balíčků](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Po chybějících souborech balíčku zobrazit tlačítko pro obnovení balíčku
Když otevřete dialogové okno konzoly Správce balíčků nebo správce balíčků NuGet, nástroj NuGet zkontroluje, jestli aktuální řešení nemá povolený režim obnovení balíčku, a jestli ve složce chybí nějaké soubory balíčku `packages` . Pokud jsou splněné tyto dvě podmínky, NuGet vás upozorní a zobrazí pohodlné tlačítko obnovení. Po kliknutí na toto tlačítko se spustí NuGet pro obnovení všech chybějících balíčků.

![Tlačítko pro obnovení balíčku v dialogovém okně](./media/packagerestore-dialog.png)

![Tlačítko pro obnovení balíčku v konzole](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Přidat soubor packages.config na úrovni řešení
V předchozích verzích NuGet má každý projekt `packages.config` soubor, který uchovává přehled o tom, jaké balíčky NuGet jsou v projektu nainstalované. Na úrovni řešení ale neexistuje žádný podobný soubor, aby bylo možné sledovat balíčky na úrovni řešení. V důsledku toho neexistuje žádný způsob, jak obnovit balíčky na úrovni řešení.
Tato funkce je nyní implementována v NuGet 1,7. Soubor na úrovni řešení `packages.config` je umístěn pod `.nuget` složkou v části kořen řešení a bude ukládat pouze balíčky na úrovni řešení.

### <a name="remove-new-package-command"></a>Příkaz Remove New-Package
Z důvodu nízkého využití se odebral příkaz New-Package. Pro vytváření balíčků doporučujeme vývojářům použít nuget.exe nebo praktického Průzkumníka balíčků NuGet.

## <a name="bug-fixes"></a>Opravy chyb
Sada NuGet 1,7 opravila mnoho chyb kolem pracovního postupu obnovení balíčku a scénářů správy sítě a zdrojů.

Úplný seznam pracovních položek opravených v NuGet 1,7 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
