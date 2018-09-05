---
title: Zpráva k vydání verze NuGet 2.7.2
description: Zpráva k vydání verze pro NuGet 2.7.2 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3e63944a05f66d5dadf17c5d4b91d3bc4478bb33
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550067"
---
# <a name="nuget-272-release-notes"></a>Zpráva k vydání verze NuGet 2.7.2

[Zpráva k vydání verze NuGet 2.7.1](../release-notes/nuget-2.7.1.md) | [zpráva k vydání verze NuGet 2.8](../release-notes/nuget-2.8.md)

NuGet 2.7.2 byla vydána 11. listopadu 2013.

## <a name="noteworthy-bug-fixes-and-features"></a>Opravy chyb zajímavosti a funkce

### <a name="license-text"></a>Text licence
Poměrně nějakou dobu je k dispozici balíčky NuGet pro několik oblíbených open source knihoven v rámci výchozích šablon pro projekty webových aplikací v sadě Visual Studio. dobře známé příkladem tohoto typu knihovna je pravděpodobně jQuery. Z důvodu podpory smlouvy přidružené k součástem, které se dodávají spolu s produktem soubor skriptu balíčku obsahuje jiné licenční text než soubor skriptu nalezen ve stejném balíčku na nuget.org veřejné galerie. Tento rozdíl v textu může zabránit aktualizace balíčků řízení v důsledku textové bloky jiné licenční způsobí soubory skriptů hodnoty jinou hodnotu hash obsahu (a proto jsou považovány za upravovat v rámci projektu).

Chcete-li tento problém zmírnit, NuGet 2.7.2 umožňuje autorovi skriptu zahrnout textový blok licencí v rámci speciálně označené části, která vypadá takto.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

Při aktualizaci balíčky s obsahem soubory, které obsahují tento blok NuGet není faktor obsahu bloku v porovnání s verzí v galerii NuGet a může proto odstranění a aktualizace obsahu souboru jakoby odpovídá původní kopírování.

Tento blok je identifikován text "NUGET: začněte licence TEXT" a "NUGET: ukončení licence TEXT" ke kterým dochází kdekoli na počátku a ukončení řádků.  Žádné formátování požadavky nejsou, umožňuje tato funkce, který se má použít z libovolného typu souboru bez ohledu na jazyk.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Přidat přesměrování vazby sestavení – bez rozhraní
Pro sestavení, které jsou součástí rozhraní .NET Framework NuGet přeskočí přidání přesměrování vazby do konfiguračního souboru aplikace při aktualizaci balíčku. Tato oprava řeší Regrese v 2.7 NuGet, kterým přesměrování vazby nebyly přidává pro některá sestavení, i když tato sestavení nejsou považovány za součást rozhraní .NET Framework. NuGet 2.7.2 obnoví předchozí 2.5 NuGet a 2.6 chování a přidá přesměrování vazby.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Instalaci přenosné knihovny se nainstalované nástroje Xamarin
Když Xamarin vývojové nástroje jsou nainstalovány na počítači, jejich upravit konfigurační data podporované architektury k určení kompatibility mezi existující kombinace cílového rozhraní framework a rozhraní Xamarin. Verze 2.7.2 NuGet je vědět, tato pravidla implicitní kompatibility a proto usnadňuje vývojářům cílení na platformy Xamarin nainstalovat přenosných knihoven, které jsou kompatibilní s Xamarinem, ale nejsou explicitně označené jako takové v balíčku metadata, samotného.

### <a name="machine-wide-configuration-settings-honored"></a>Nastavení konfigurace celý počítač, neuplatňují
Při použití souborů hierarchické Nuget.Config, repositoryPath klíč není respektováno pro soubory na soubor Nuget.Config co nejblíže ke kořenu řešení. NuGet v sadě Visual Studio 2013, nainstaluje vlastní soubor Nuget.Config v %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config Chcete-li přidat zdroj balíčku "A Microsoft .NET". V důsledku toho řešení pro použití vlastního repositoryPath v řešení se odstranit soubor Nuget.Config úrovni počítače - také znamená odebráním zdroje balíčku "A Microsoft .NET". NuGet 2.7.2 nyní ctí prioritu pravidla pro repositoryPath při použití souborů hierarchické souboru Nuget.Config.

## <a name="all-changes"></a>Všechny změny
Úplný seznam pracovních položek opravených NuGet 2.7.2, prosím zobrazení [NuGet sledování problémů pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
