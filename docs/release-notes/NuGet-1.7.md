---
title: Poznámky k verzi 1.7 NuGet
description: Zpráva k vydání verze pro NuGet 1.7, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551464"
---
# <a name="nuget-17-release-notes"></a>Poznámky k verzi 1.7 NuGet

[Zpráva k vydání verze NuGet 1.6](../release-notes/nuget-1.6.md) | [zpráva k vydání verze NuGet 1.8](../release-notes/nuget-1.8.md)

NuGet 1.7 byla vydána 4. dubna 2012.

## <a name="known-installation-issue"></a>Instalace známý problém
Pokud spustíte VS 2010 SP1, můžete narazit na chybu instalace při pokusu o upgradu Nugetu, pokud máte nainstalovaný starší verze.

Alternativním řešením je jednoduše odinstalovat NuGet a nainstalujte ho z Galerie rozšíření VS.  Zobrazit [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Další informace.

Poznámka: Pokud Visual Studio neumožní odinstalovat rozšíření (tlačítko Odinstalovat je vypnutá), pak pravděpodobně nutné restartovat Visual Studio pomocí příkazu "Spustit jako správce."

## <a name="features"></a>Funkce

### <a name="support-opening-readmetxt-file-after-installation"></a>Podpora otevírání souboru readme.txt po instalaci
Novinka v 1.7, pokud balíček obsahuje `readme.txt` souboru v kořenovém adresáři balíčku NuGet se automaticky otevře tento soubor po dokončení instalace balíčku.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Zobrazit v dialogovém okně Spravovat balíčky NuGet balíčky předběžné verze balíčků
Dialogové okno Spravovat balíčky NuGet nyní obsahuje rozevírací seznam, který poskytuje možnost zobrazit předběžné verze balíčků.

![Zobrazuje předběžné verze balíčků](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Zobrazit tlačítko pro obnovení balíčků, když nebyly nalezeny soubory balíčku
Pokud otevřete konzolu Správce balíčků nebo balíčky NuGet správce dialogového okna, NuGet zkontroluje, pokud se aktuální řešení má povolený režim obnovení balíčků a v případě, že všechny soubory v balíčku chybí `packages` složky. Pokud tyto dvě podmínky jsou splněny, NuGet vás upozorní a zobrazí pohodlný tlačítko Obnovit. Kliknutím na toto tlačítko spustí obnovit všechny chybějící balíčky NuGet.

![Tlačítko Obnovit balíček v dialogovém okně](./media/packagerestore-dialog.png)

![Tlačítko Obnovit balíček v konzole](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Přidat soubor packages.config úrovni řešení
V předchozích verzích balíčku nuget, má každý projekt `packages.config` souboru, který uchovává informace o jaké balíčky NuGet jsou nainstalované v daném projektu. Na úrovni řešení k udržení přehledu o balíčcích úrovni řešení byla však žádný podobně jako soubor. V důsledku toho neexistoval způsob, jak k obnovení balíčků úrovni řešení.
Tato funkce je nyní implementována v NuGet 1.7. Úroveň řešení `packages.config` soubor umístěn v rámci `.nuget` ve složce řešení kořenové a budou ukládat balíčky pouze úrovni řešení.

### <a name="remove-new-package-command"></a>Odebrat příkaz New-Package
Z důvodu s nízkým využitím byl odebrán příkazu New-Package. Vývojáři se doporučuje použít k vytváření balíčků nuget.exe nebo po ruce Průzkumníku balíčků NuGet.

## <a name="bug-fixes"></a>Opravy chyb
NuGet 1.7 chyba opravena řada chyb kolem pracovního postupu obnovení balíčků a scénáře řízení síťového nebo zdroje.

Úplný seznam pracovních položek opravených NuGet 1.7 prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
