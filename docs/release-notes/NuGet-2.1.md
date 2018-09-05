---
title: Poznámky k verzi 2.1 NuGet
description: Zpráva k vydání verze NuGet 2.1, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548594"
---
# <a name="nuget-21-release-notes"></a>Poznámky k verzi 2.1 NuGet

[Zpráva k vydání verze NuGet 2.0](../release-notes/nuget-2.0.md) | [zpráva k vydání verze NuGet 2.2](../release-notes/nuget-2.2.md)

NuGet 2.1 byla vydána 4. října 2012.

## <a name="hierarchical-nugetconfig"></a>Hierarchické soubor Nuget.Config

NuGet 2.1 získáte větší flexibilitu při řízení nastavení NuGet prostřednictvím rekurzivně walking nahoru strukturu složek hledání `NuGet.Config` soubory a pak sestavení konfigurace ze sady všechny nalezené soubory.  Jako příklad vezměte v úvahu scénář, ve kterém má tým jako interní balíček úložiště pro průběžné integrované sestavení další vnitřní závislosti. Struktura složek pro jednotlivé projekt může vypadat nějak takto:

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

Kromě toho pokud obnovení balíčků je povolená pro řešení, do následující složky budou také existovat:

    C:\myteam\solution1\.nuget

Abyste měli úložiště interní balíček týmu k dispozici pro všechny projekty, které tým pracuje na, zároveň nejsou k dispozici pro každý projekt na počítači, můžeme vytvořte nový soubor Nuget.Config a umístěte ho do složky c:\myteam. Neexistuje žádný způsob pro zadejte složku balíčků každý projekt.

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

Můžeme nyní vidět, že byl přidán zdroj spuštěním příkazu 'nuget.exe zdroje' z libovolné složky pod c:\myteam jak je znázorněno níže:

![Zdroje balíčků z konfigurace nadřazené nuget](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` soubory se vyhledávají v následujícím pořadí:

1. `.nuget\Nuget.Config`
2. Provede rekurzivní ze složky projektu do kořenového adresáře
3. Globální `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

Tyto konfigurace se než v použít *pořadí*, to znamená, že podle výše uvedených řazení, globální Nuget.Config by být použije první, za nímž následuje zjištěných Nuget.Config soubory z kořenového adresáře do složky projektu, a potom podle `.nuget\Nuget.Config`.  To je zvlášť důležité, pokud používáte `<clear/>` prvek, který chcete odebrat z konfigurace sady položek.

## <a name="specify-packages-folder-location"></a>Zadejte "balíčků' umístění složky

V minulosti má NuGet se spravovaným balíčků řešení ze složky známé "packages" nalezena pod kořenové složky řešení.  Pro vývojové týmy, které mají mnoho různých řešení, které mají nainstalované balíčky NuGet to může způsobit stejného balíčku instaluje v mnoha různých míst v systému souborů.

NuGet 2.1 poskytuje podrobnější kontrolu nad umístění složky balíčků prostřednictvím `repositoryPath` prvek `NuGet.Config` souboru.  Staví na předchozí příklad podporu hierarchických Nuget.Config, se předpokládá, že chceme mít všechny projekty v rámci C:\myteam\ sdílet stejnou složku balíčků.  K tomu jednoduše přidejte následující položku do `c:\myteam\Nuget.Config`.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

V tomto příkladu, sdílený `Nuget.Config` souboru určuje sdílených balíčků složku pro každý projekt, který je vytvořen pod C:\myteam, bez ohledu na to hloubku. Poznámka: Pokud máte existující složku balíčků pod kořenového adresáře řešení, musíte odstranit ho před NuGet umístí balíčky v novém umístění.

## <a name="support-for-portable-libraries"></a>Podpora pro přenosné knihovny

[Přenosné knihovny](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) je funkce zavedená pomocí rozhraní .NET 4, která umožňuje vytvářet sestavení, které budou fungovat bez úprav na různých platformách společnosti Microsoft, od verzí rozhraní.NET Framework pro Silverlight pro Windows Phone a Xbox i 360 (i když se v tuto chvíli nepodporuje NuGet cílové Xbox přenosné knihovny).  Tím, že rozšíří [balíček konvence](../create-packages/supporting-multiple-target-frameworks.md) profilů a verze rozhraní framework NuGet 2.1 teď podporuje přenosných knihoven tím, že vám vytvořit balíčky, které mají složené framework a profil cílového `lib` složek.

Jako příklad zvažte následující knihovny přenosných tříd k dispozici cílové platformy.

![Dialogové okno Vytvoření přenosné knihovny](./media/releasenotes-21-plib.png)

Po sestavení knihovny a příkaz `nuget.exe pack MyPortableProject.csproj` spuštění nové přenosné knihovny struktury složky balíčku můžou vidět zkoumání obsahu vygenerovaný balíček NuGet.

![Přenosná knihovna rozložení balíčku](./media/releasenotes-21-plib-layout.png)

Jak je vidět, konvence název složky přenosné knihovny odpovídá vzoru "portable-{framework 1} + {framework n}" kde identifikátory framework použijte existující [konvence název a verzi rozhraní framework](../reference/target-frameworks.md). Jedinou výjimkou konvence názvem a verzí se nachází v rámci identifikátor použitý pro Windows Phone.  Tento zástupný název by měl použít název rozhraní "wp" (wp7, wp71 nebo wp8). Použití "wp7 silverlight", například způsobí chybu.

Při instalaci balíčku, který je vytvořen z tuto strukturu složek, NuGet teď používat jeho rozhraní framework a profil pravidla více cílů, jak je uvedeno ve složce s názvem.  Za pravidla pro porovnávání NuGet je Princip "konkrétnější" cíle má přednost před těmi "specifické pro less".  To znamená, že monikery cílení na konkrétní platformu vždy upřednostňované nad přenosné ty Pokud jsou oba kompatibilní s projektem.  Kromě toho pokud více přenosné cíle jsou kompatibilní s projektem, NuGet preferovali jeden, kde je "nejbližší" do projektu balíček odkazování na sadu podporované platformy.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Cílení na Windows 8 a Windows Phone 8 projekty

Kromě přidání podpory pro cílení na projekty přenosných knihoven, NuGet 2.1 poskytuje nové rozhraní framework monikery pro projekty Windows Store 8 a Windows Phone 8, jakož i některé nové obecné monikery pro Windows Store a Windows Phone projekty, které budou snazší správa v budoucích verzích příslušné platformy.

Identifikátory pro aplikace Windows Store 8 vypadat takto:

| NuGet 2.0 a starší | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45, .NETCore45 | Windows, Windows8, Windows, win8 |

<br/>
Pro projekty Windows Phone identifikátory vypadat takto:

| Phone OS | NuGet 2.0 a starší | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-wp | webové části, WindowsPhone7 wp7 WindowsPhone, |
| Windows Phone 7.5 (Mango) | silverlight4 wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (nepodporováno) | wp8, WindowsPhone8 |

<br/>
Ve všech výše uvedené změny bude nadále staré názvy framework plné podpory společností NuGet 2.1.  V budoucnu, nové názvy by měla sloužit jako, v budoucích verzích příslušné platformy bude stabilnější. Nové názvy se *není* se nepodporuje v verze NuGet starší než 2.1, ale to podle toho naplánujte pro případ přechod usnadní.

## <a name="improved-search-in-package-manager-dialog"></a>Vylepšené vyhledávání v dialogovém okně Správce balíčků

V posledních několika iterací změny byly zavedeny do Galerie NuGet, který výrazně zlepšit rychlost a relevance vyhledávání balíčků.  Nicméně tato vylepšení byla omezena na webu nuget.org.  NuGet 2.1 zpřístupňuje vylepšené vyhledávání prostředí přes dialogové okno Správce balíčků NuGet.  Jako příklad Představte si, že byste chtěli najít balíček ve verzi Preview ukládání do mezipaměti na Windows Azure.  "Azure Cache" může být rozumné vyhledávací dotaz pro tento balíček.  V předchozích verzích dialogové okno Správce balíčků nebude požadovaný balíček i uvedena na první stránku výsledků.  Ale v NuGet 2.1 požadovaný balíček nyní zobrazí v horní části výsledků vyhledávání.

![Hledání dialogové okno Správce balíčků](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Vynucení aktualizace balíčku

Před NuGet 2.1 NuGet by přeskočit aktualizace balíčku, pokud došlo a nikoli číslo vyšší číslo verze.  To zavedené případná problémová místa pro určité scénáře – zejména v případě sestavení nebo CI scénáře, ve kterém tým nechtěli zvyšovat číslo každé sestavení verze balíčku.  Chcete vynutit aktualizaci bez ohledu na to je požadované chování.  NuGet 2.1 řeší to s příznakem "přeinstalovat".  Například předchozí verze balíčku nuget by výsledkem bylo toto při pokusu o aktualizaci balíčku, který nemá novější verze balíčku:

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

S příznakem reinstall bude aktualizován balíček bez ohledu na to, zda je k dispozici novější verze.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

Jiný scénář, kde prokáže příznak reinstall výhodné je znovu cílení rozhraní. Při změně cílové rozhraní projektu (například z .NET 4 na rozhraní .NET 4.5), Update-Package-přeinstalujte můžete aktualizovat odkazy na správné sestavení pro všechny balíčky NuGet v projektu nainstalován.

## <a name="edit-package-sources-within-visual-studio"></a>Upravit zdroje balíčků v rámci sady Visual Studio

V předchozích verzích balíčku nuget aktualizuje se zdroj balíčku z v rámci dialogové okno Možnosti sady Visual Studio vyžaduje odstranit a znovu přidat zdroj balíčku.  NuGet 2.1 Tento pracovní postup zlepšuje podporu aktualizace jako funkce první třídy uživatelské rozhraní konfigurace.

![Dialogové okno Konfigurace Správce balíčků](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Opravy chyb

NuGet 2.1 obsahuje řadu oprav chyb. Úplný seznam pracovních položek opravených NuGet 2.0 prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
