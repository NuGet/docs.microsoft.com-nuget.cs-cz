---
title: Poznámky k verzi 1.8 NuGet
description: Zpráva k vydání verze pro NuGet 1.8, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ff6d12606b1bed479e63eebccd978ff9cd4a7faf
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546618"
---
# <a name="nuget-18-release-notes"></a>Poznámky k verzi 1.8 NuGet

[Zpráva k vydání verze NuGet 1.7](../release-notes/nuget-1.7.md) | [zpráva k vydání verze NuGet 2.0](../release-notes/nuget-2.0.md)

23. května 2012 byla vydána NuGet 1.8.

## <a name="known-installation-issue"></a>Instalace známý problém
Pokud spustíte VS 2010 SP1, můžete narazit na chybu instalace při pokusu o upgradu Nugetu, pokud máte nainstalovaný starší verze.

Alternativním řešením je jednoduše odinstalovat NuGet a nainstalujte ho z Galerie rozšíření VS.  Zobrazit [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Další informace nebo [přejděte přímo na opravu hotfix VS](http://bit.ly/vsixcertfix).

Poznámka: Pokud Visual Studio neumožní odinstalovat rozšíření (tlačítko Odinstalovat je vypnutá), pak pravděpodobně nutné restartovat Visual Studio pomocí příkazu "Spustit jako správce."

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 kompatibilní s Windows XP, opravy hotfix publikování

Krátce po vydání NuGet 1.8, jsme zjistili, že kryptografie změny ve verzi 1.8 se podařilo přerušit uživatelé Windows XP.

Od té doby jsme vydali opravu hotfix, která řeší tento problém.  Aktualizací NuGet prostřednictvím Galerie rozšíření sady Visual Studio, dostanete tuto opravu hotfix.

## <a name="features"></a>Funkce

### <a name="satellite-packages-for-localized-resources"></a>Satelitní balíčky pro lokalizované prostředky
NuGet 1.8 teď podporuje možnost vytvářet samostatné balíčky pro lokalizované prostředky, podobně jako funkce satelitní sestavení rozhraní .NET Framework.  Satelitní balíček je vytvořen stejným způsobem jako jakýkoli jiný balíček NuGet a uveďte několik konvence:

* Satelitní balíček ID a název souboru by měla obsahovat příponu, která odpovídá jednomu z standardní [jazyková verze řetězce používané rozhraním .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).
* V jeho `.nuspec` souboru satelitní balíčku by měl definovat prvek jazyka s stejný řetězec jazykové verze použita v ID
* Satelitní balíčku by měl definovat v závislosti na jeho `.nuspec` souboru na základní balíček, který je jednoduše balíček se stejným ID minus přípony jazyka.  Základní balíček musí být k dispozici v úložišti pro úspěšnou instalaci.

Instalace balíčku s lokalizované prostředky, vývojář explicitně vybere balíček lokalizované z úložiště. V současné době neposkytuje Galerie NuGet jakékoliv zvláštní zacházení satelitní balíčky.

![Dialogové okno Správce balíčků s lokalizované pacakges](./media/dlg-w-loc-packs.png)

Protože satelitní balíček obsahuje závislost na jeho základní balíček, satelitních i základní balíčky jsou načetli do složky balíčků NuGet a nainstalovat.

![Složka balíčky s lokalizovaných balíčků](./media/fldr-loc-packs.png)

Při instalaci balíčku satelit, navíc NuGet také rozpozná zásady vytváření názvů řetězec jazykové verze a pak zkopíruje lokalizovaný prostředek sestavení do správné podsložku v rámci balíčku core, takže mohou být zachyceny pomocí rozhraní .NET Framework.

![Základní složka balíčku se složkou zkopírovaný prostředek](./media/fldr-copied-loc.png)

Jednu existující chybu k mějte na paměti s balíčky satelitní je, že NuGet nekopíruje lokalizované prostředky `bin` složku pro webové projekty.  Tento problém bude vyřešen v příští verzi balíčku nuget.

Ukazuje, jak vytvořit a používat balíčky satelitní úplnou ukázku najdete v tématu [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Souhlas obnovení balíčku
Ve verzi 1.8 NuGet můžeme podle připravovat základy pro podporu důležité omezení pro obnovení balíčku ochrana osobních údajů uživatelů. Toto omezení vyžaduje vývojáři, kteří vytvářejí projekty a řešení, které jsou výslovně souhlas k obnovení balíčků pomocí obnovení balíčků je přechod do režimu online stáhnout balíčky z nakonfigurovaných balíček zdrojů.

Zadejte svůj souhlas 2 způsoby. První najdete v okně balíček Správce konfigurace jak je znázorněno níže.  Tato metoda je primárně určena pro počítače pro vývojáře.

![Dialogové okno Konfigurace Správce balíčků](./media/pr-consent-configdlg.png)

Druhý způsob je nastavit proměnné "EnableNuGetPackageRestore" prostředí na hodnotu "true".  Tato metoda je určena pro počítače bezobslužného jako jsou třeba servery CI nebo sestavení.

Nyní jak bylo uvedeno výš, mají jsme pouze podle připravovat základy pro tuto funkci ve verzi 1.8 NuGet.  Prakticky to znamená, že když jsme přidali veškerou logiku k povolení této funkce, vynutí se aktuálně v této verzi. Bude povoleno, ale v další verzi balíčku nuget, takže jsme chtěli jste ho vědět co nejdříve tak, aby se může správně nakonfigurovat vaše prostředí a proto nebude ovlivněné až začneme vynutit omezení souhlas.

Další podrobnosti najdete [příspěvek na blogu týmu](http://blog.nuget.org/20120518/package-restore-and-consent.html) o této funkci.

### <a name="nugetexe-performance-improvements"></a>Vylepšení výkonu nuget.exe
Změnou instalačního příkazu ke stažení a instalaci balíčků současně přináší NuGet 1.8 výraznému zlepšení výkonu nuget.exe – a obnovení balíčků rozšíření.  Vysoké úrovně testování ukazuje, že ve verzi 1.8 NuGet asi o 35 % zlepšuje výkon pro instalaci balíčků 6 do projektu.  Zvýšení počtu balíčků do 25 ukazuje výkonnější o 60 %.

## <a name="bug-fixes"></a>Opravy chyb
NuGet 1.8 obsahuje několik oprav chyb s důrazem na konzole Správce balíčků a pracovní postup obnovení balíčků, zejména souvisí se obnovení balíčku vyjádření souhlasu a integrace Express pro Windows 8.
Úplný seznam pracovních položek opraveno ve verzi 1.8 NuGet prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
