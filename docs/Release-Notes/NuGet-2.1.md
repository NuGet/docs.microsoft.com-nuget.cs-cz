---
title: Poznámky k verzi 2.1 NuGet
description: Poznámky k verzi pro NuGet 2.1 včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3b7a000098a7362f4b1c2c4072c6cd1468baf9b5
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-21-release-notes"></a>Poznámky k verzi 2.1 NuGet

[Poznámky k verzi NuGet 2.0](../release-notes/nuget-2.0.md) | [NuGet 2.2 poznámky k verzi](../release-notes/nuget-2.2.md)

4. října 2012 byla vydána NuGet 2.1.

## <a name="hierarchical-nugetconfig"></a>Hierarchická soubor nuget.config.

NuGet 2.1 vám dává větší flexibilitu při řízení nastavení NuGet prostřednictvím rekurzivně proti si strukturu složek hledání `NuGet.Config` soubory a pak vytváření konfigurace ze sady všech nalezených souborů.  Jako příklad vezměte v úvahu scénář, kde má tým úložiště interní balíčků pro položky konfigurace sestavení z jiných vnitřní závislosti. Struktura složek pro jednotlivé projekt může vypadat následovně:

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

Kromě toho pokud obnovení balíčku je povolená pro řešení, do následující složky budou existovat také:

    C:\myteam\solution1\.nuget

Aby bylo možné používat úložiště na interní balíčků tým služby, které jsou k dispozici pro všechny projekty, které tým funguje, při není ji dáte k dispozici pro každý projekt na počítači, můžeme vytvoření nového souboru Nuget.Config a umístěte jej do složky c:\myteam. Neexistuje žádný způsob, jak na určením složku balíčků pro projekt.

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

Teď vidíme, že byl přidán zdroj spuštěním příkazu 'nuget.exe zdroje' z libovolné složky pod c:\myteam jak je uvedeno níže:

![Zdroje balíčků z konfigurace nadřazené nuget](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` soubory jsou vyhledávány v následujícím pořadí:

1. `.nuget\Nuget.Config`
2. Provede rekurzivní ze složky projektu kořenovou
3. Globální `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

Tyto konfigurace se než použijí v *pořadí*, znamená to, že je založeno na výše uvedené pořadí, globální Nuget.Config by se použije první, následuje zjištěných Nuget.Config soubory z kořenové složky projektu, a potom podle `.nuget\Nuget.Config`.  To je zvlášť důležité, pokud používáte `<clear/>` elementu, který chcete odebrat sadu položek z konfigurace.

## <a name="specify-packages-folder-location"></a>Zadejte umístění složky ' balíčky.

V minulosti má NuGet spravované balíčků řešení ze složky známé, balíčky, nalezeno pod kořenové složky řešení.  Pro vývojové týmy, které mají mnoho různých řešení, které mají nainstalované balíčky NuGet to může způsobit ve stejném balíčku instaluje na mnoha různých místech v systému souborů.

NuGet 2.1 poskytuje podrobnější kontrolu nad umístění složky balíčky prostřednictvím `repositoryPath` element v `NuGet.Config` souboru.  Vytváření v předchozím příkladu hierarchické Nuget.Config podpory, předpokládá, že chceme mít všechny projekty v části C:\myteam\ sdílet stejnou složku balíčků.  K tomu jednoduše přidejte následující položku na `c:\myteam\Nuget.Config`.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

V tomto příkladu sdílený `Nuget.Config` soubor Určuje balíčky sdílené složky pro každý projekt, který se vytvoří pod C:\myteam, bez ohledu na to hloubka. Poznámka: Pokud máte existující balíčky složce pod kořenového adresáře řešení, budete muset odstranit před NuGet umístí balíčky v novém umístění.

## <a name="support-for-portable-libraries"></a>Podpora pro přenosné knihovny

[Přenosné knihovny](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) je funkce poprvé .NET 4, který vám umožní sestavovat sestavení, které můžete pracovat bez úprav na různých platformách Microsoft, z verzí rozhraní.NET Framework pro Silverlight pro Windows Phone a i Xbox 360 (i když v současné době nepodporuje NuGet cíl přenosné knihovny Xbox).  Tím, že rozšíří [balíček konvence](../create-packages/supporting-multiple-target-frameworks.md) profilů a framework verze NuGet 2.1 teď podporuje přenosné knihovny tím, že vám vytvořit balíčky, které mají složené framework a profil cíle `lib` složek.

Jako příklad zvažte následující knihovny přenosných tříd dostupných cílových platforem.

![Dialogové okno Vytvoření přenosné knihovny](./media/releasenotes-21-plib.png)

Jakmile je vytvořen knihovny a příkaz `nuget.exe pack MyPortableProject.csproj` běží, nové přenositelností struktura složek balíček knihovny můžete zobrazit tak, že prověří obsah vygenerovaný balíček NuGet.

![Přenosná knihovna balíček rozložení](./media/releasenotes-21-plib-layout.png)

Jak vidíte, konvence název složky přenosné knihovny se následující 'přenosné-{framework 1} + {framework n}' kde identifikátory framework podle existující [framework název a verze konvence](../reference/target-frameworks.md). Jedinou výjimkou konvence název a verzi nachází v identifikátoru framework se používá pro Windows Phone.  Tato Přezdívka měli použít název rozhraní "wp" (wp7, wp71 nebo wp8). Pomocí "silverlight-wp7", například bude výsledkem chyba.

Při instalaci balíčku, který je vytvořený z této struktura složek, NuGet nyní pravidla můžete použít jeho framework a profil pro více cílů, jako je zadaný v názvu složky.  Za pravidel porovnávání NuGet je Princip "konkrétnější" cíle má přednost před "méně specifických".  To znamená, že monikery cílení na konkrétní platformu vždy upřednostňované přes přenosné ty Pokud jsou oba kompatibilní s projektem.  Kromě toho pokud víc přenosného cíle jsou kompatibilní s projektem, NuGet přednost jeden, kde je "nejbližší" do projektu balíček odkazování na sadu platformy podporované.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Cílení Windows 8 a Windows Phone 8 projekty

Kromě přidání podpory pro cílení na přenosné knihovny projekty, NuGet 2.1 poskytuje nové monikery framework pro projekty úložiště systému Windows 8 a Windows Phone 8, jakož i některé nové obecné zástupných názvů pro Windows Store a Windows Phone projekty, které budou snazší správa v budoucích verzích příslušné platformy.

Pro aplikace pro Windows 8 Store identifikátory vypadat takto:

| NuGet 2.0 a starší | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45, .NETCore45 | Windows, Windows8, win, win8 |

<br/>
Pro projekty Windows Phone identifikátorů vypadat takto:

| Phone OS | NuGet 2.0 a starší | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-wp | webové části, WindowsPhone7 wp7, WindowsPhone, |
| Windows Phone 7.5 (Mango) | silverlight4 wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (není podporována) | wp8, WindowsPhone8 |

<br/>
Ve všech výše uvedených změny budou nadále původní názvy framework plně podporovat NuGet 2.1.  Klouzavý dopředu, nové názvy je třeba použít jak budou stabilnější v budoucích verzích příslušné platformy. Nové názvy bude *není* se nepodporuje ve verzích NuGet před 2.1, ale, takže podle toho naplánovat pro případ, aby přepínač.

## <a name="improved-search-in-package-manager-dialog"></a>Vylepšené vyhledávání v dialogovém okně Správce balíčků

Změny byly zavedeny v posledních několika iterací, do Galerie NuGet, který výrazně Vylepšená rychlost a relevance balíček hledání.  Tato vylepšení byly však omezeny na nuget.org Web.  NuGet 2.1 zpřístupňuje vylepšené vyhledávání prostředí prostřednictvím dialogové okno Správce balíčků NuGet.  Jako příklad Představte si, že jste chtěli najít balíček Windows Azure ukládání do mezipaměti Preview.  Přiměřené vyhledávací dotaz pro tento balíček může být "Azure Cache".  V předchozích verzích dialogové okno Správce balíčku nebude požadovaný balíček uvedený i na první stránce výsledků.  Ale v NuGet 2.1 požadované balíčku se zobrazí v horní části výsledků vyhledávání.

![Balíček správce dialogové okno hledání](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Vynucení aktualizace balíčku

Před 2.1 NuGet, které by NuGet přeskočit aktualizace balíčku, pokud došlo není číslo vysoké verze.  To se zavedl třecí pro určité scénáře – zejména v případě sestavení nebo CI scénáře, kde týmem nechtěli se zvýší číslo s každé sestavení verze balíčku.  Toto chování žádoucí bylo vynutit aktualizaci bez ohledu na to.  NuGet 2.1 řeší to s příznakem 'přeinstalujte'.  Předchozí verze NuGet například by způsobilo následující při pokusu o aktualizaci balíčku, který neměl novější verze balíčku:

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

S příznakem přeinstalovat, bude aktualizován balíček bez ohledu na to, jestli existuje novější verze.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

Jiné scénáře, kde prokáže výhodné příznak přeinstalovat je, že znovu cílových framework. Při změně cílový framework projektu (například z .NET 4 na rozhraní .NET 4.5), balíček aktualizace-přeinstalujte můžete aktualizovat odkazy na správné sestavení pro všechny balíčky NuGet, které jsou nainstalované v projektu.

## <a name="edit-package-sources-within-visual-studio"></a>Upravit zdroje balíčků ve Visual Studiu

V předchozích verzích NuGet aktualizace zdroj balíčku z v rámci dialogové okno Možnosti sady Visual Studio vyžaduje odstranění a znovu přidat zdroj balíčku.  Podpora aktualizace jako první třídy funkce uživatelského rozhraní pro konfiguraci zlepšuje NuGet 2.1 Tento pracovní postup.

![Dialogové okno Konfigurace správce balíčku](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Opravy chyb

NuGet 2.1 obsahuje opravy mnoha chyb. Úplný seznam pracovní položky pevná ve NuGet 2.0, prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
