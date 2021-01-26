---
title: Zpráva k vydání verze NuGet 2,2
description: Poznámky k verzi pro NuGet 2,2, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780436"
---
# <a name="nuget-22-release-notes"></a>Zpráva k vydání verze NuGet 2,2

Zpráva k [vydání verze](../release-notes/nuget-2.1.md)  |  NuGet 2,1 [Poznámky k verzi NuGet 2.2.1](../release-notes/nuget-2.2.1.md)

NuGet 2,2 byl vydaný 12. prosince 2012.

## <a name="visual-studio-quick-launch"></a>Snadné spuštění sady Visual Studio
Jednou z nových funkcí, které byly přidány v aplikaci Visual Studio 2012, bylo [dialogové okno snadné spuštění](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). NuGet 2,2 rozšiřuje toto dialogové okno, aby bylo možné inicializovat dialog správce balíčků s hledanými výrazy uvedenými v panelu snadného spuštění. Například když zadáte jQuery v okně rychlé spuštění, ve výsledcích se zobrazí možnost vyhledat balíčky NuGet, které odpovídají "jQuery".

![Balíčky NuGet v aplikaci Visual Studio – snadné spuštění](./media/quick-launch.png)

Výběrem této možnosti se spustí standardní možnosti vyhledávání správce balíčků NuGet pro termín "jQuery".

![Dialog správce balíčků NuGet předem naplněný](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Zadat celou složku pro obsah balíčku
NuGet 2,2 teď umožňuje zadat celou složku v `<file>` prvku `.nuspec` souboru, aby zahrnovala celý obsah této složky. Například následující příkaz způsobí, že všechny skripty ve složce Scripts balíčku budou přidány do složky contents\scripts při instalaci balíčku do projektu.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Aktualizace 6/24/16: prázdné složky ve složce Content se při instalaci balíčku ignorují.**

## <a name="known-issues"></a>Známé problémy

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Instalace balíčku pro projekty F # při použití konzoly Správce balíčků se nezdařila
Při pokusu o instalaci balíčku NuGet do projektu F # pomocí konzoly Správce balíčků je vyvolána událost InvalidOperationException. Aktivně spolupracujeme s týmem F # k vyřešení problému, ale mezitím je k dispozici alternativní řešení pro instalaci balíčků NuGet do projektů F # prostřednictvím dialogového okna Správce balíčků NuGet místo konzoly. [Další informace jsou k dispozici na webu CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Opravy chyb
NuGet 2,2 obsahuje mnoho oprav chyb. Úplný seznam pracovních položek opravených v NuGet 2,2 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
