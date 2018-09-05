---
title: Zpráva k vydání verzí 1.6 verze NuGet
description: Zpráva k vydání verze pro NuGet 1.6, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549009"
---
 # <a name="nuget-16-release-notes"></a>Zpráva k vydání verzí 1.6 verze NuGet

[Zpráva k vydání verze NuGet 1.5](../release-notes/nuget-1.5.md) | [zpráva k vydání verze NuGet 1.7](../release-notes/nuget-1.7.md)

NuGet 1.6 byla vydána 13. prosince 2011.

## <a name="known-installation-issue"></a>Instalace známý problém
Pokud spustíte VS 2010 SP1, můžete narazit na chybu instalace při pokusu o upgradu Nugetu, pokud máte nainstalovaný starší verze.

Alternativním řešením je jednoduše odinstalovat NuGet a nainstalujte ho z Galerie rozšíření VS.  Zobrazit [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Další informace.

Poznámka: Pokud Visual Studio neumožní odinstalovat rozšíření (tlačítko Odinstalovat je vypnutá), pak pravděpodobně nutné restartovat Visual Studio pomocí příkazu "Spustit jako správce."

## <a name="features"></a>Funkce

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Podporu pro Semantic Versioning a předběžné verze balíčků
NuGet 1.6 zavádí podporu pro Semantic Versioning (SemVer). Další informace o tom, jak používá SemVer najdete [dokumentace ke službě správy verzí](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Pomocí nástroje NuGet bez vrácení se změnami balíčky (obnovení balíčku)
NuGet 1.6 teď nabízí prvotřídní podporu pro pracovní postup, ve které NuGet balíčky nejsou přidány do správy zdrojových kódů, ale místo toho se obnoví v okamžiku sestavení Pokud chybí. Další podrobnosti najdete v článku [pomocí NuGet bez potvrzení balíčky do správy zdrojových kódů](../consume-packages/packages-and-source-control.md) tématu.

### <a name="item-templates-that-install-nuget-packages"></a>Šablony položek, které instalují balíčky NuGet
Staví na práce, která podporují předinstalovaný balíček NuGet do šablony projektů Visual Studio, NuGet 1.6 přidává podporu pro položku šablony sady Visual Studio. Šablony položek mohou být přidruženy balíčky NuGet, které jsou nainstalovány při vyvolání šablony.

Další informace o tom, jak změnit šablonu projektu/položky k instalaci balíčků NuGet najdete [balíčky v šablony sady Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) tématu.

### <a name="support-for-disabling-package-sources"></a>Podpora pro zakázání zdroje balíčků
Po nakonfigurování více zdrojů balíčku NuGet bude vypadat v každém z nich balíčky během instalace balíčku a jeho závislosti. Zdroj balíčku, který je mimo provoz z nějakého důvodu může vážně pomalé dolů NuGet.

Před NuGet 1.6 může odebrat zdrojový balíček, ale pak je nutné pamatovat si podrobnosti o kdy budete chtít přidat zpátky v.

NuGet 1.6 umožňuje zrušením zaškrtnutí zdroj balíčku, který ji zakázat, ale zachovat kolem.

![Zakázat balíček](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Opravy chyb
NuGet 1.6 bylo celkem 106 pracovní položky opraveno. 95 z nich byly klasifikovány jako chyby a 10 z nich byly funkce.

Úplný seznam pracovních položek opravených NuGet 1.6 prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
