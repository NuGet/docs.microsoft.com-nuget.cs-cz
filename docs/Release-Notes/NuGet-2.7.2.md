---
title: "Poznámky k verzi NuGet 2.7.2 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro NuGet 2.7.2 včetně – známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 2.7.2 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8fe9acc3ad9c1c368fc750694ea523ac845995c5
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-272-release-notes"></a>Poznámky k verzi NuGet 2.7.2

[Poznámky k verzi NuGet 2.7.1](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 poznámky k verzi](../release-notes/nuget-2.8.md)

NuGet 2.7.2 byla vydána 11 listopadu 2013.

## <a name="noteworthy-bug-fixes-and-features"></a>Pozoruhodné oprav chyb a funkce

### <a name="license-text"></a>Licence textu
Celkem nějakou dobu je k dispozici balíčky NuGet pro několik oblíbených knihovny open-source jako součást výchozí šablony pro projekty webových aplikací v sadě Visual Studio. jQuery je pravděpodobně dobře známé příklad tohoto typu knihovny. Z důvodu podpory smlouvu přidružené součásti, které se dodávají spolu s produktem soubor skriptu balíčku obsahuje jiné licenční text než soubor skriptu v galerii veřejné nuget.org nalezen ve stejném balíčku. Tento rozdíl v textu můžete zabránit v balíčku aktualizace budete pokračovat v důsledku bloky textu jiné licenční způsobuje soubory skriptu jinou hodnotu hash obsahu hodnoty (a proto jsou považovány za upraveno v rámci projektu).

Ke zmírnění tohoto problému, NuGet 2.7.2 umožňuje autorovi skriptu zahrnout bloku textu licencí v rámci speciálně označen jako část, která vypadá takto.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

Při aktualizaci balíčky s obsahem soubory obsahující tento blok NuGet není zohlednit obsahu bloku v porovnání s verzí v galerii NuGet a můžete proto odstranit a aktualizovat soubor obsahu, jako kdyby odpovídá původní kopie.

Tento blok je identifikována text "NUGET: začněte licence TEXT" a "NUGET: END licence TEXT" výskytu kdekoli na začátku a končí řádky.  Žádné formátování požadavky nejsou, povolení této funkce lze použít v libovolného typu souboru text bez ohledu na jazyk.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Přidejte přesměrování vazby sestavení – bez architektury
Pro sestavení, které jsou součástí rozhraní .NET Framework NuGet přeskočí přidání přesměrování vazby do konfiguračního souboru aplikace při aktualizaci balíčku. Tato oprava řeší Regrese v 2.7 NuGet, které přesměrování vazby nebyly přidávané pro některé sestavení, i když tyto sestavení nejsou považovány za součást rozhraní .NET Framework. NuGet 2.7.2 obnoví předchozí 2.5 NuGet a 2.6 chování a přidá přesměrování vazby.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Instalace přenosné knihovny s nainstalovanými nástroji pro Xamarin
Při instalaci nástrojů pro vývoj na Xamarin na počítači se upravit konfigurační data podporované architektury k určení kompatibilitu mezi existující cílový framework kombinace a Xamarin rozhraní. S verzí 2.7.2 NuGet má teď informace o těchto pravidel implicitní kompatibility a proto umožňuje snadné pro vývojáře cílené na platformách Xamarin pro instalaci přenosné knihovny, které jsou kompatibilní s Xamarinem, ale není explicitně označené jako takový v balíčku metadata sám sebe.

### <a name="machine-wide-configuration-settings-honored"></a>Nastavení konfigurace celého systému dodržení
Při použití souborů hierarchické Nuget.Config, nebyl se klíč repositoryPath dodržení pro soubory Nuget.Config nejbližší do kořenového adresáře řešení. NuGet v sadě Visual Studio 2013, nainstaluje vlastního souboru Nuget.Config v %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config Chcete-li přidat zdroj balíčku "A Microsoft .NET". V důsledku toho řešení pro použití vlastního repositoryPath v řešení se odstranit úroveň počítače Nuget.Config – to také znamená odebrání zdroji balíčku "A Microsoft .NET". NuGet 2.7.2 teď ctí prioritu pravidla pro repositoryPath při použití souborů hierarchické Nuget.Config.

## <a name="all-changes"></a>Všechny změny
Úplný seznam pracovní položky pevná ve NuGet 2.7.2, prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
