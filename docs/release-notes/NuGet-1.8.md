---
title: Poznámky k verzi 1,8 NuGet
description: Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 1.8 NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1801d62b786717c088429fbeca6f1f72f5ab6b4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820100"
---
# <a name="nuget-18-release-notes"></a>Poznámky k verzi 1,8 NuGet

[Poznámky k verzi NuGet 1.7](../release-notes/nuget-1.7.md) | [NuGet 2.0 poznámky k verzi](../release-notes/nuget-2.0.md)

NuGet 1.8 byla vydána 23 květen 2012.

## <a name="known-installation-issue"></a>Instalace známý problém
Pokud používáte VS 2010 SP1, můžete spustit došlo k chybě instalace při pokusu o upgrade NuGet, pokud máte nainstalovaný starší verze.

Alternativní řešení je jednoduše odinstalovat NuGet a nainstalujte ji z Galerie rozšíření VS.  V tématu [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Další informace, nebo [přejděte přímo na opravu hotfix VS](http://bit.ly/vsixcertfix).

Poznámka: Pokud Visual Studio nebude možné odinstalovat rozšíření (k dispozici tlačítko Odinstalovat), bude pravděpodobně nutné restartujte Visual Studio pomocí "Spustit jako správce."

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 kompatibilní se systémem Windows XP, opravy hotfix publikována

Krátce po vydání byl NuGet 1.8, zjistili jsme, že ke změně šifrování v 1.8 překročila uživatelé v systému Windows XP.

Protože Vydali jsme opravu hotfix, která řeší tento problém.  Při aktualizaci NuGet prostřednictvím Galerie rozšíření sady Visual Studio, zobrazí se tato oprava hotfix.

## <a name="features"></a>Funkce

### <a name="satellite-packages-for-localized-resources"></a>Satelitní balíčky pro místní zdroje
NuGet 1.8 teď podporuje možnost vytvořit samostatné balíčky pro místní zdroje, podobně jako možnosti satelitní sestavení rozhraní .NET Framework.  Satelitní balíček je vytvořen stejným způsobem jako jakýkoli jiný balíček NuGet s přidáním systému několik konvence:

* Satelitní balíček ID a název souboru by měla obsahovat příponu, která odpovídá jednomu z standardní [jazykovou verzi řetězců v rozhraní .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).
* V jeho `.nuspec` souboru balíčku satelitní měli definovat element jazyka s do jednoho řetězce jazykovou verzi, která je použita v ID
* Balíček satelitní měli definovat v závislosti na jeho `.nuspec` souboru do jeho základní balíčku, který je jednoduše balíček se stejným ID minus příponou jazyk.  Základní balíček musí být k dispozici v úložišti pro úspěšnou instalaci.

Chcete-li nainstalovat balíček s lokalizované prostředky, vývojář explicitně vybere lokalizované balíček z úložiště. V současné době Galerie NuGet není poskytnuta jakýkoli druh zvláštní zacházení satelitní balíčků.

![Dialogové okno Správce balíčku se lokalizované pacakges](./media/dlg-w-loc-packs.png)

Vzhledem k tomu, že balíček satelitní uvádí závislost na jeho základní balíček, jsou satelitní i základní balíčky vyžádat do složky balíčků NuGet a nainstalovat.

![Složka balíčky s lokalizované balíčky](./media/fldr-loc-packs.png)

Při instalaci balíčku satelit, navíc NuGet také rozpozná zásady vytváření názvů řetězce jazykovou verzi a pak zkopíruje lokalizovaný prostředek sestavení do správné podsložky v rámci balíčku jádra, takže mohou být zachyceny pomocí rozhraní .NET Framework.

![Základní složka balíčku s složku zkopírovaný prostředků](./media/fldr-copied-loc.png)

Jeden existující chyby na mějte na paměti, satelitní balíčků je, že NuGet nekopíruje lokalizované prostředky k `bin` složku pro webové projekty.  Tento problém bude vyřešený v příští verzi balíčku nuget.

Kompletní příklad, který ukazuje, jak vytvořit a používat satelitní balíčky, najdete v části [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Balíček obnovení souhlasu
V NuGet 1.8 jsme umístěné základ pro podporu důležité omezení pro obnovení balíčků pro ochrany osobních údajů uživatele. Toto omezení vyžaduje vývojářům vytvářet projekty a řešení, které používáte obnovení balíčků pro výslovně souhlasit s obnovení balíčků je přechod do režimu online na stahovat balíčky ze zdroje balíčků nakonfigurované.

Zadejte svůj souhlas 2 způsoby. První naleznete v dialogu balíček Správce konfigurace jak je uvedeno níže.  Tato metoda je primárně určený pro vývojáře počítače.

![Dialogové okno Konfigurace správce balíčku](./media/pr-consent-configdlg.png)

Druhý způsob je nastavení prostředí proměnné "EnableNuGetPackageRestore" na hodnotu "true".  Tato metoda je určena pro bezobslužné počítače, jako jsou třeba servery položky konfigurace nebo sestavení.

Nyní jak jsme uvedli výše, budeme mít pouze podle základ pro tuto funkci NuGet 1.8.  Prakticky to znamená, že když jsme přidali veškerou logiku k povolení této funkce, vynuceno není aktuálně v této verzi. Bude povoleno, ale v příští verzi NuGet, takže jsme chtěli, aby vás upozornit je co nejdříve, aby správně nakonfigurovat vaše prostředí a proto nelze dopad jsme spouštění vynutit omezení souhlasu.

Další podrobnosti najdete v tématu [příspěvku na blogu týmu](http://blog.nuget.org/20120518/package-restore-and-consent.html) na tuto funkci.

### <a name="nugetexe-performance-improvements"></a>Vylepšení výkonu nuget.exe
Změnou instalační příkaz stáhnout a nainstalovat balíčky současně přináší NuGet 1.8 výraznému zlepšení výkonu k nuget.exe – a obnovení balíčků rozšíření.  Vysoké úrovně testování ukazuje výkon pro instalaci 6 balíčky do projektu volbou asi 35 % v NuGet 1.8.  Zvýšením počtu balíčků, které mají 25 uvádí výkonnější o 60 %.

## <a name="bug-fixes"></a>Opravy chyb
NuGet 1.8 obsahuje několik oprav chyb s důrazem na konzole Správce balíčků a pracovní postup obnovení balíčku, zvlášť, protože se týká balíček obnovení souhlasu a integrace s Windows 8 Express.
Úplný seznam pracovní položky pevná ve NuGet 1.8 prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
