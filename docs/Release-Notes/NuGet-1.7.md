---
title: "Poznámky k verzi NuGet 1.7 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: df7becc6-993d-4d06-8495-a0c26748bdfa
description: "Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 1.7 NuGet."
keywords: "NuGet 1.7 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 420b40576cb3862f0e4406966f9ccca9fd1f39a1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-17-release-notes"></a>Poznámky k verzi 1.7 NuGet

[Poznámky k verzi NuGet 1.6](../release-notes/nuget-1.6.md) | [NuGet 1.8 poznámky k verzi](../release-notes/nuget-1.8.md)

NuGet 1.7 byla vydána 4. dubna 2012.

## <a name="known-installation-issue"></a>Instalace známý problém
Pokud používáte VS 2010 SP1, můžete spustit došlo k chybě instalace při pokusu o upgrade NuGet, pokud máte nainstalovaný starší verze.

Alternativní řešení je jednoduše odinstalovat NuGet a nainstalujte ji z Galerie rozšíření VS.  V tématu [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) Další informace.

Poznámka: Pokud Visual Studio nebude možné odinstalovat rozšíření (k dispozici tlačítko Odinstalovat), bude pravděpodobně nutné restartujte Visual Studio pomocí "Spustit jako správce."

## <a name="features"></a>Funkce

### <a name="support-opening-readmetxt-file-after-installation"></a>Podporuje otevření souboru readme.txt po instalaci
Novinka v 1.7, pokud obsahuje váš balíček `readme.txt` soubor v kořenovém adresáři balíčku NuGet se automaticky otevře tento soubor po dokončení instalace vašeho balíčku.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Zobrazit v dialogovém okně Spravovat balíčky NuGet balíčky předběžné verze balíčků
Dialogové okno Spravovat balíčky NuGet nyní zahrnuje rozevírací nabídce, která poskytuje možnost zobrazit předběžné verze balíčků.

![Zobrazuje předběžné verze balíčků](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Obnovení balíčků tlačítko zobrazit, když jsou soubory balíčku chybí
Pokud otevřete konzolu Správce balíčků nebo NuGet Správce balíčků dialogové okno, zkontrolujte Pokud současné řešení má povolen režim obnovení balíčků NuGet a v případě, že všechny soubory v balíčku chybí `packages` složky. Pokud jsou tyto dvě podmínky splněny, NuGet vás upozorní a zobrazí pohodlný tlačítko obnovení. Kliknutím na toto tlačítko spustí NuGet obnovit všechny chybějící balíčky.

![Tlačítko Obnovit balíček v dialogovém okně](./media/packagerestore-dialog.png)

![Tlačítko Obnovit balíčku v konzole](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Přidejte soubor packages.config úrovni řešení
V předchozích verzích NuGet, každý projekt má `packages.config` souboru, který uchovává informace o jaké balíčky NuGet jsou nainstalované v tomto projektu. Na úrovni řešení ke sledování řešení úrovni balíčky se však žádný podobně jako soubor. V důsledku toho se žádný způsob, jak obnovení balíčků řešení úrovni.
Tato funkce se teď implementuje v NuGet 1.7. Úroveň řešení `packages.config` soubor je umístěn v `.nuget` ve složce řešení kořenový uživatel a uloží pouze řešení na úrovni balíčků.

### <a name="remove-new-package-command"></a>Odeberte příkaz nového balíčku
Z důvodu nízkém zatížení byla odebrána příkaz nový balíček. Vývojáři se doporučuje použít k vytvoření balíčků nuget.exe nebo užitečný Průzkumníka balíček NuGet.

## <a name="bug-fixes"></a>Opravy chyb
NuGet 1.7 má vyřešili mnoho chyb kolem scénáře sítě nebo zdrojového kódu a pracovní postup obnovení balíčků.

Úplný seznam pracovní položky pevná ve NuGet 1.7 prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
