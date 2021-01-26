---
title: Zpráva k vydání verze NuGet 1,8
description: Poznámky k verzi pro NuGet 1,8, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8dd0fff88424c516d8b894412d07dcc53af19265
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777102"
---
# <a name="nuget-18-release-notes"></a>Zpráva k vydání verze NuGet 1,8

Zpráva k [vydání verze](../release-notes/nuget-1.7.md)  |  NuGet 1,7 Zpráva k [vydání verze NuGet 2,0](../release-notes/nuget-2.0.md)

NuGet 1,8 byla vydána 23. května 2012.

## <a name="known-installation-issue"></a>Známý problém s instalací
Pokud používáte VS 2010 SP1, můžete při pokusu o upgrade NuGetu v případě, že máte nainstalovanou starší verzi, spustit chybu instalace.

Alternativním řešením je jednoduše odinstalovat NuGet a pak ji nainstalovat z galerie rozšíření VS.  Další informace najdete v tématu <https://support.microsoft.com/kb/2581019> , kde najdete další informace, nebo [přejděte přímo na opravu hotfix vs](http://bit.ly/vsixcertfix).

Poznámka: Pokud Visual Studio neumožní odinstalovat rozšíření (tlačítko Odinstalace je zakázané), pak budete pravděpodobně muset restartovat Visual Studio pomocí možnosti Spustit jako správce.

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1,8 nekompatibilní se systémem Windows XP, byla publikována oprava hotfix

Krátce po vydání NuGet 1,8 jsme zjistili, že se v systému Windows XP změnila kryptografie v 1,8 podařilo přerušit Users.

Od této verze jsme vydali opravu hotfix, která tento problém řeší.  Když aktualizujete NuGet přes Galerii rozšíření sady Visual Studio, obdržíte tuto opravu hotfix.

## <a name="features"></a>Funkce

### <a name="satellite-packages-for-localized-resources"></a>Satelitní balíčky pro lokalizované prostředky
NuGet 1,8 teď podporuje možnost vytvářet samostatné balíčky pro lokalizované prostředky, podobně jako satelitní možnosti sestavení .NET Framework.  Satelitní balíček se vytvoří stejným způsobem jako jakýkoli jiný balíček NuGet s přidáním několika konvencí:

* ID satelitního balíčku a název souboru by měly obsahovat příponu, která odpovídá jednomu z [řetězců standardní jazykové verze používané .NET Framework](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).
* V jeho `.nuspec` souboru by měl satelitní balíček definovat prvek jazyka se stejným řetězcem kultury použitým v ID.
* Satelitní balíček by měl v souboru definovat závislost `.nuspec` na jeho základní balíček, který je jednoduše balíčkem se STEJNÝM ID minus přípona jazyka.  Pro úspěšnou instalaci musí být v úložišti k dispozici základní balíček.

Pro instalaci balíčku s lokalizovanými prostředky vývojář explicitně vybere lokalizovaný balíček z úložiště. V současnosti galerie NuGet neposkytuje žádný druh speciálního zacházení pro satelitní balíčky.

![Dialog správce balíčků s lokalizovaným pacakges](./media/dlg-w-loc-packs.png)

Vzhledem k tomu, že satelitní balíček uvádí závislost na svůj základní balíček, balíčky Satellite i Core jsou načteny do složky balíčků NuGet a nainstalovány.

![Složka balíčků s lokalizovanými balíčky](./media/fldr-loc-packs.png)

Kromě toho při instalaci satelitního balíčku NuGet také rozpoznává konvenci pojmenování řetězců jazykové verze a pak zkopíruje lokalizované sestavení prostředků do správné podsložky v rámci balíčku Core tak, aby mohl být vyzvednut .NET Framework.

![Základní složka balíčku s zkopírovanou složkou prostředků](./media/fldr-copied-loc.png)

Jedna existující chyba při poznámení s satelitními balíčky je, že NuGet nekopíruje lokalizované prostředky do `bin` složky pro webové projekty.  Tento problém bude vyřešen v příští verzi NuGet.

Úplný příklad, jak vytvořit a používat satelitní balíčky, najdete v tématu [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample) .

### <a name="package-restore-consent"></a>Souhlas s obnovením balíčku
V NuGet 1,8 jsme nazákladyi na podporu důležitých omezení pro obnovení balíčků, abyste chránili ochranu osobních údajů uživatelů. Toto omezení vyžaduje, aby vývojáři vytvářející projekty a řešení, které používají obnovení balíčků, explicitně souhlasili s tím, že přecházejí do online režimu a stáhli balíčky z konfigurovaných zdrojů balíčků.

Existují dva způsoby, jak tento souhlas poskytnout. První najdete v dialogovém okně Konfigurace Správce balíčků, jak je znázorněno níže.  Tato metoda je primárně určena pro vývojářské počítače.

![Dialogové okno Konfigurace Správce balíčků](./media/pr-consent-configdlg.png)

Druhou metodou je nastavit proměnnou prostředí "EnableNuGetPackageRestore" na hodnotu "true".  Tato metoda je určená pro bezobslužné počítače, jako jsou CI nebo servery sestavení.

Jak je uvedeno výše, pouze základy pro tuto funkci v NuGet 1,8.  Prakticky to znamená, že zatímco jsme přidali veškerou logiku, která tuto funkci povoluje, není v tuto chvíli Tato verze vynutila. V příští verzi NuGet ho ale budete chtít, abychom si ho měli co nejdříve vědět, abyste mohli svoje prostředí vhodně nakonfigurovat, a proto nebude mít dopad na to, když začneme vyhovět omezením souhlasu.

Další podrobnosti najdete v [příspěvku na blogu týmu](http://blog.nuget.org/20120518/package-restore-and-consent.html) na této funkci.

### <a name="nugetexe-performance-improvements"></a>Vylepšení výkonu nuget.exe
Díky úpravě instalačního příkazu pro paralelní stažení a instalaci balíčků přináší NuGet 1,8 výrazné zlepšení výkonu nuget.exe – a při obnovení balíčku rozšíření.  Testování na vysoké úrovni ukazuje, že výkon pro instalaci 6 balíčků do projektu se zlepšuje přibližně o 35% ve NuGet 1,8.  Zvýšení počtu balíčků na 25 znázorňuje nárůst výkonu o 60%.

## <a name="bug-fixes"></a>Opravy chyb
NuGet 1,8 obsahuje poměrně několik oprav chyb s důrazem na konzolu Správce balíčků a pracovní postup obnovení balíčku, zejména v případě, že se týká souhlasu s obnovením balíčků a integrace s Windows 8 Express.
Úplný seznam pracovních položek opravených v NuGet 1,8 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).