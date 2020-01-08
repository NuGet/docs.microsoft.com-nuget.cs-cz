---
title: Zpráva k vydání verze NuGet 1,6
description: Poznámky k verzi pro NuGet 1,6, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2878d3809b2be4fb71f4e7b1a1e08e405ead44b9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384134"
---
 # <a name="nuget-16-release-notes"></a>Zpráva k vydání verze NuGet 1,6

[Poznámky k verzi nuget 1,5](../release-notes/nuget-1.5.md) | zpráva k [vydání verze NuGet 1,7](../release-notes/nuget-1.7.md)

NuGet 1,6 byl vydán 13. prosince 2011.

## <a name="known-installation-issue"></a>Známý problém s instalací
Pokud používáte VS 2010 SP1, můžete při pokusu o upgrade NuGetu v případě, že máte nainstalovanou starší verzi, spustit chybu instalace.

Alternativním řešením je jednoduše odinstalovat NuGet a pak ji nainstalovat z galerie rozšíření VS.  Další informace naleznete v tématu <https://support.microsoft.com/kb/2581019>.

Poznámka: Pokud Visual Studio neumožní odinstalovat rozšíření (tlačítko Odinstalace je zakázané), pak budete pravděpodobně muset restartovat Visual Studio pomocí možnosti Spustit jako správce.

## <a name="features"></a>Funkce

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Podpora sémantických verzí a předprodejních balíčků
NuGet 1,6 zavádí podporu pro sémantickou správu verzí (SemVer). Další podrobnosti o tom, jak používá SemVer, najdete v [dokumentaci ke správám verzí](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Použití NuGet bez vrácení se změnami balíčků (obnovení balíčku)
NuGet 1,6 teď má jako první podporu pro pracovní postup, ve kterém se balíčky NuGet nepřidaly do správy zdrojových kódů, ale v době, kdy chybí, se místo toho obnoví v čase sestavení. Pokud chcete získat další informace, přečtěte si téma [použití NuGet bez potvrzení balíčků do správy zdrojového kódu](../consume-packages/packages-and-source-control.md) .

### <a name="item-templates-that-install-nuget-packages"></a>Šablony položek, které instalují balíčky NuGet
Sada NuGet 1,6 také přidává podporu šablon položek sady Visual Studio, která je postavena na práci pro podporu předinstalovaného balíčku NuGet do šablon projektů sady Visual Studio. K šablonám položek můžou být přidružené balíčky NuGet, které se nainstalují při vyvolání šablony.

Další informace o tom, jak změnit šablonu projektu nebo položky pro instalaci balíčků NuGet, najdete v tématu [balíčky v tématu šablony sady Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) .

### <a name="support-for-disabling-package-sources"></a>Podpora pro zakázání zdrojů balíčků
Pokud je nakonfigurováno více zdrojů balíčků, bude NuGet při instalaci balíčku a jeho závislostech Hledat v každém z nich pro balíčky. Zdroj balíčku, který je mimo provoz z nějakého důvodu, může vážně zpomalit NuGet.

Před verzí NuGet 1,6 byste mohli odebrat zdroj balíčku, ale pak si musíte pamatovat podrobnosti o tom, kdy ho chcete přidat zpátky do.

NuGet 1,6 umožňuje zrušit kontrolu zdroje balíčku, abyste ho zakázali, ale zachovali si ho.

![Zakázání balíčku](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Opravy chyb
Aktualizace NuGet 1,6 obsahovala celkem 106 pracovních položek. 95 z nich bylo klasifikováno jako chyby a 10 z nich bylo funkcí.

Úplný seznam pracovních položek opravených v NuGet 1,6 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
