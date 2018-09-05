---
title: Poznámky k verzi 2.2 NuGet
description: Zpráva k vydání verze pro NuGet 2.2 včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545989"
---
# <a name="nuget-22-release-notes"></a>Poznámky k verzi 2.2 NuGet

[Zpráva k vydání verze NuGet 2.1](../release-notes/nuget-2.1.md) | [zpráva k vydání verze NuGet 2.2.1](../release-notes/nuget-2.2.1.md)

12. prosince 2012 byla vydána NuGet 2.2.

## <a name="visual-studio-quick-launch"></a>Snadné spuštění sady Visual Studio
Mezi nové funkce přidané v sadě Visual Studio 2012 byl [dialogové okno Snadné spuštění](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). NuGet 2.2 rozšiřuje toto dialogové okno, což umožňuje inicializovat dialogové okno Správce balíčků s hledaným výrazům zadali rychlé uvedení na trh. Například zadání 'jquery' v panelu Snadné spuštění nyní zahrnuje možnost ve výsledcích hledání balíčků NuGet odpovídajících řetězci "jquery".

![NuGet v sadě Visual Studio snadného spuštění](./media/quick-launch.png)

Výběrem této možnosti se spustí standardní NuGet package manager vyhledávání pro termín "jquery".

![Dialogové okno Správce balíčků NuGet předvyplněný](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Zadejte celou složku pro obsah balíčku
NuGet 2.2 teď umožňuje zadat celou složku v `<file>` elementu `.nuspec` soubor obsahovat veškerý obsah této složky. Například následující způsobí, že všechny skripty ve složce balíčku skripty mají být přidány do složky contents\scripts při instalaci balíčku do projektu.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Aktualizace 6/24/16: prázdné složky ve složce "obsah" jsou ignorovány při instalaci balíčku.**

## <a name="known-issues"></a>Známé problémy

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Selhání instalace balíčku pro projekty F # při používání konzoly Správce balíčků
Při pokusu o instalaci balíčku NuGet do projektu F # pomocí konzoly Správce balíčků, je vyvolána výjimka InvalidOperationException. Aktivně Pracujeme s týmem F # k vyřešení problému, ale do té doby alternativním řešením je instalace balíčků NuGet do projektů F # přes dialogové okno Správce balíčků NuGet, nikoli konzole. [Další informace jsou k dispozici na webu CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Opravy chyb
NuGet 2.2 zahrnuje opravy mnoha chyb. Úplný seznam pracovních položek opravených NuGet 2.2 prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
