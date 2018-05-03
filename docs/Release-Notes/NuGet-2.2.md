---
title: Poznámky k verzi 2.2 NuGet
description: Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 2.2 NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 21f212de53da5faf1ec0762f97a840968b615b19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-22-release-notes"></a>Poznámky k verzi 2.2 NuGet

[Poznámky k verzi NuGet 2.1](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 poznámky k verzi](../release-notes/nuget-2.2.1.md)

NuGet 2.2 byla vydána 12 prosinec 2012.

## <a name="visual-studio-quick-launch"></a>Snadné spuštění sady Visual Studio
Mezi nové funkce, které byl přidán v sadě Visual Studio 2012 byla [dialogové okno Snadné spuštění](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). NuGet 2.2 rozšiřuje toto dialogové okno, díky kterému jej k chybě při inicializaci dialogové okno Správce balíčku s podmínkami vyhledávání zadané v Snadné spuštění. Například zadáte, jquery, snadné spuštění nyní zahrnuje možnost ve výsledcích hledání balíčků NuGet odpovídající 'jquery'.

![NuGet v sadě Visual Studio snadné spuštění](./media/quick-launch.png)

Výběrem této možnosti se spustí standardní NuGet balíček správce možnosti vyhledávání pro termín 'jquery'.

![Dialogové okno Správce balíčků NuGet předem vyplněná](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Zadejte celou složku pro obsah balíčku
NuGet 2.2 teď umožňuje zadat celou složku v `<file>` element `.nuspec` souboru celý obsah této složky. Například následující způsobí, že všechny skripty ve složce balíčku skripty mají být přidány do složky contents\scripts při instalaci balíčku do projektu.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Aktualizace 6/24/16: prázdné složky ve složce "obsah" ignorují při instalaci balíčku.**

## <a name="known-issues"></a>Známé problémy

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Při použití konzoly Správce balíčků selže instalace balíčku pro projekty F #
Při pokusu o instalaci balíčku NuGet do projektu aplikace F # pomocí konzoly Správce balíčků, je vyvolána výjimkou InvalidOperationException. Aktivně Pracujeme s týmem F # k vyřešení problému, ale do té doby, řešením je instalace balíčků NuGet do projektů F # přes dialogové okno Správce balíčků NuGet spíše než konzole. [Další informace najdete na webu CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Opravy chyb
NuGet 2.2 obsahuje opravy mnoha chyb. Úplný seznam pracovní položky pevné v NuGet 2.2 prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
