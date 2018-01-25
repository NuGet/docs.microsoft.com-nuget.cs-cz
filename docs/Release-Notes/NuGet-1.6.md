---
title: "Poznámky k verzi NuGet 1.6 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 1.6 NuGet."
keywords: "NuGet 1.6 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 114b03cede24dee520ace1d8aa920a648ad16af1
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
 # <a name="nuget-16-release-notes"></a>Poznámky k verzi 1.6 verzi NuGet

[Poznámky k verzi NuGet 1.5](../release-notes/nuget-1.5.md) | [NuGet 1.7 poznámky k verzi](../release-notes/nuget-1.7.md)

NuGet 1.6 byla vydána 13 prosince 2011.

## <a name="known-installation-issue"></a>Instalace známý problém
Pokud používáte VS 2010 SP1, můžete spustit došlo k chybě instalace při pokusu o upgrade NuGet, pokud máte nainstalovaný starší verze.

Alternativní řešení je jednoduše odinstalovat NuGet a nainstalujte ji z Galerie rozšíření VS.  V tématu [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) Další informace.

Poznámka: Pokud Visual Studio nebude možné odinstalovat rozšíření (k dispozici tlačítko Odinstalovat), bude pravděpodobně nutné restartujte Visual Studio pomocí "Spustit jako správce."

## <a name="features"></a>Funkce

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Podpora pro sémantické verze a předběžné verze balíčků
NuGet 1.6 zavádí podporu pro sémantické verze (SemVer). Další informace o tom, jak ji používá SemVer, přečtěte si [Správa verzí dokumentace](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Pomocí nástroje NuGet bez kontroly v balíčcích (obnovení balíčku)
NuGet 1.6 teď nabízí prvotřídní podporu pro pracovní postup v který NuGet balíčky nejsou přidány do správy zdrojového kódu, ale místo toho jsou obnoveny v čase vytvoření buildu Pokud chybí. Další informace najdete [pomocí NuGet bez potvrzení balíčky do správy zdrojového kódu](../consume-packages/packages-and-source-control.md) tématu.

### <a name="item-templates-that-install-nuget-packages"></a>Šablony položek, které instalace balíčků NuGet
Sestavování na práci pro podporu předinstalované balíček NuGet do projektu šablony sady Visual Studio, NuGet 1.6 přidává podporu pro šablony sady Visual Studio položky. Šablony položek může mít přidružené balíčky NuGet, které jsou nainstalovány při vyvolání šablony.

Další informace o tom, jak změnit šablonu projektu/položky instalace balíčků NuGet najdete [balíčky v šablony sady Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) tématu.

### <a name="support-for-disabling-package-sources"></a>Podpora pro zakázání zdroje balíčků
Po nakonfigurování více zdrojů balíčku NuGet Hledat v každé z nich pro balíčky během instalace balíček a jeho závislosti. Zdroj balíčku, která je mimo provoz z nějakého důvodu může vážně pomalu dolů NuGet.

Před NuGet 1.6 by mohl odebrat zdroje balíčku, ale pak je nutné pamatovat na to, podrobnosti o když chcete přidat ji zpátky.

NuGet 1.6 umožňuje zdroj balíčku, který ji zakázat, ale je udržovat kolem zaškrtnutí políčka.

![Zakázání balíčku](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Opravy chyb
NuGet 1.6 měl celkem 106 pracovní položky, které jsou pevné. 95 těchto byly klasifikovány jako chyby a 10 těchto byly funkce.

Úplný seznam pracovní položky pevná ve NuGet 1.6 prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
