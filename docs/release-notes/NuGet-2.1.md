---
title: Zpráva k vydání verze NuGet 2,1
description: Poznámky k verzi pro NuGet 2,1, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777032"
---
# <a name="nuget-21-release-notes"></a>Zpráva k vydání verze NuGet 2,1

Zpráva k [vydání verze](../release-notes/nuget-2.0.md)  |  NuGet 2,0 Zpráva k [vydání verze NuGet 2,2](../release-notes/nuget-2.2.md)

NuGet 2,1 byl vydán 4. října 2012.

## <a name="hierarchical-nugetconfig"></a>Hierarchické Nuget.Config

NuGet 2,1 poskytuje větší flexibilitu při řízení nastavení NuGet pomocí způsobu rekurzivního procházení struktury složek, která hledá `NuGet.Config` soubory a pak sestaví konfiguraci ze sady všech nalezených souborů.  Můžete například zvážit scénář, ve kterém má tým interní úložiště balíčků pro sestavení CI jiných interních závislostí. Struktura složky pro jednotlivý projekt může vypadat takto:

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

Kromě toho, pokud je pro řešení povoleno obnovení balíčku, bude také k dispozici následující složka:

```
C:\myteam\solution1\.nuget
```

Aby bylo k dispozici interní úložiště balíčků týmu pro všechny projekty, na kterých tým pracuje, a ne tak, aby byl k dispozici pro každý projekt v počítači, můžeme vytvořit nový soubor Nuget.Config a umístit ho do složky c:\myteam. Neexistuje žádný způsob, jak určit složku balíčků pro každý projekt.

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

Teď vidíte, že byl zdroj přidaný, spuštěním příkazu nuget.exe sources z jakékoli složky pod c:\myteam, jak je znázorněno níže:

![Zdroje balíčků z nadřazené konfigurace NuGet](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` soubory jsou vyhledány v následujícím pořadí:

1. `.nuget\Nuget.Config`
2. Rekurzivní procházení ze složky projektu do kořenového adresáře
3. Globální `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )

Konfigurace jsou nepoužitelné v *obráceném pořadí*, což znamená, že na základě výše uvedeného řazení by se nejdřív použily globální Nuget.Config a za ním byly zjištěné Nuget.Config soubory z kořenové složky do složky projektu `.nuget\Nuget.Config` .  To je obzvláště důležité, pokud používáte `<clear/>` element k odebrání sady položek z konfigurace.

## <a name="specify-packages-folder-location"></a>Zadejte umístění složky Packages.

V minulosti měl NuGet spravované balíčky řešení ze známé složky Packages, která se nachází pod kořenovou složkou řešení.  Pro vývojové týmy, které mají nainstalovanou spoustu různých řešení s nainstalovanými balíčky NuGet, to může mít za následek instalaci stejného balíčku na mnoho různých míst v systému souborů.

NuGet 2,1 poskytuje podrobnější kontrolu nad umístěním složky Packages prostřednictvím `repositoryPath` elementu v `NuGet.Config` souboru.  Při sestavování v předchozím příkladu hierarchické podpory Nuget.Config Předpokládejme, že chceme, aby všechny projekty v rámci C:\myteam\ sdílely stejnou složku balíčků.  K tomu stačí přidat následující položku do `c:\myteam\Nuget.Config` .

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

V tomto příkladu sdílený `Nuget.Config` soubor Určuje složku sdílené balíčky pro každý projekt, který je vytvořen pod C:\myteam, bez ohledu na hloubku. Všimněte si, že pokud máte složku s balíčky pod kořenem řešení, je nutné ji odstranit předtím, než NuGet umístí balíčky do nového umístění.

## <a name="support-for-portable-libraries"></a>Podpora přenosných knihoven

[Přenosné knihovny](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) jsou funkce, která je nejprve představena s rozhraním .NET 4, která umožňuje sestavit sestavení, která mohou fungovat bez úprav na různých platformách společnosti Microsoft, od verzí The.NET Framework po Silverlight až po Windows Phone a dokonce i Xbox 360 (i když v tuto chvíli nástroj NuGet nepodporuje cíl přenosové knihovny Xbox).  Rozšířením [konvencí](../create-packages/supporting-multiple-target-frameworks.md) pro verze a profily architektury balíčků NuGet 2,1 teď podporuje přenosné knihovny tím, že vám umožní vytvářet balíčky, které mají složené architektury a cílové `lib` složky profilu.

Jako příklad zvažte následující dostupné cílové platformy knihovny přenosných tříd.

![Dialogové okno pro vytvoření přenosné knihovny](./media/releasenotes-21-plib.png)

Po vytvoření knihovny a spuštění příkazu se `nuget.exe pack MyPortableProject.csproj` může zobrazit nová struktura složky balíčku přenositelné knihovny. prozkoumáte obsah vygenerovaného balíčku NuGet.

![Rozložení balíčku přenosné knihovny](./media/releasenotes-21-plib-layout.png)

Jak vidíte, konvence názvu složky přenositelné knihovny se řídí vzorem "přenosné-{Framework 1} + {Framework n}", kde identifikátory rozhraní následují po existujícím [názvu rozhraní a konvenci verzí](../reference/target-frameworks.md). Jedna výjimka pro název a konvence verze se nachází v identifikátoru rozhraní, který se používá pro Windows Phone.  Tento moniker by měl používat název rozhraní WP (wp7, wp71 nebo WP8). Pokud například použijete ' Silverlight-WP7 ', výsledkem bude chyba.

Při instalaci balíčku vytvořeného z této struktury složek teď může NuGet použít své rozhraní a pravidla profilů na více cílů, jak je uvedeno v názvu složky.  Pravidla pro porovnání se základními balíčky NuGet jsou principem, že "konkrétnější" cíle budou mít přednost před "méně specifickými".  To znamená, že monikery cílené na konkrétní platformu budou vždy upřednostňovány přes přenosné, pokud jsou obě kompatibilní s projektem.  Kromě toho, pokud je více přenosných cílů kompatibilní s projektem, NuGet bude preferovat, kde je sada podporovaných platforem "nejbližší", k projektu, který odkazuje na balíček.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Cílení na projekty Windows 8 a Windows Phone 8

Kromě přidání podpory pro cílení na přenositelné projekty knihovny poskytuje NuGet 2,1 nové monikery rozhraní pro projekty Windows 8 Store a Windows Phone 8 a také některé nové obecné monikery pro projekty Windows Store a Windows Phone, které budou snazší spravovat v budoucích verzích příslušných platforem.

Pro aplikace Windows 8 Store tyto identifikátory vypadají takto:

| NuGet 2,0 a starší | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45,. NETCore45 | Windows, Windows8, Win, Win8 |

<br/>
Pro Windows Phone projekty identifikátory vypadají takto:

| Operační systém telefonu | NuGet 2,0 a starší | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3 – WP | WP, wp7, WindowsPhone, WindowsPhone7 |
| Windows Phone 7,5 (mango) | silverlight4-wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (Nepodporováno) | WP8, WindowsPhone8 |

<br/>
Ve všech výše uvedených změnách budou staré názvy rozhraní nadále plně podporovány NuGet 2,1.  V rámci přesunu dopředu by se nové názvy měly používat, protože budou v budoucích verzích příslušných platforem stabilnější. Nové názvy se ve verzích NuGet starších než 2,1 *nepodporují,* takže si je ale podle potřeby zajistěte, aby se tento přepínač naplánoval.

## <a name="improved-search-in-package-manager-dialog"></a>Vylepšené vyhledávání v dialogovém okně Správce balíčků

V průběhu několika předchozích iterací byly do galerie NuGet zavedeny změny, které výrazně zlepšily rychlost a závažnost prohledávání balíčku.  Tato vylepšení se ale omezila na web nuget.org.  NuGet 2,1 nabízí vylepšené možnosti vyhledávání v dialogovém okně Správce balíčků NuGet.  Představte si například, že jste chtěli najít balíček služby Windows Azure Caching Preview.  Přiměřený vyhledávací dotaz pro tento balíček může být "Azure cache".  V předchozích verzích dialogu Správce balíčků se požadovaný balíček ani na první stránce výsledků neuvádí.  V NuGet 2,1 se ale požadovaný balíček teď zobrazuje v horní části výsledků hledání.

![Hledání v dialogovém okně Správce balíčků](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Vynutit aktualizaci balíčku

Před NuGet 2,1 by NuGet přeskočil aktualizaci balíčku, pokud se nejedná o číslo vysoké verze.  Tím bylo zavedeno tření pro určité scénáře – zejména v případě scénářů sestavení nebo CI, kdy tým nechtěl zvýšit číslo verze balíčku u každého sestavení.  Požadované chování bylo vynucovat bez ohledu na aktualizaci.  NuGet 2,1 tuto adresu řeší příznakem "přeinstalace".  Například při pokusu o aktualizaci balíčku, který nemá novější verzi balíčku, by měly být v předchozích verzích NuGet následující:

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

Pomocí příznaku přeinstalace se balíček aktualizuje bez ohledu na to, jestli existuje novější verze.

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

Dalším scénářem, kdy příznak opětovného navýšení projevuje, je to, že rozhraní cílí na cílení. Při změně cílové architektury projektu (například z rozhraní .NET 4 na rozhraní .NET 4,5) může Update-Package-REINSTALL aktualizovat odkazy na správná sestavení pro všechny balíčky NuGet nainstalované v projektu.

## <a name="edit-package-sources-within-visual-studio"></a>Upravit zdroje balíčků v sadě Visual Studio

V předchozích verzích NuGet aktualizoval zdroj balíčku z dialogového okna Možnosti sady Visual Studio, které vyžaduje odstranění a opětovné přidání zdroje balíčku.  NuGet 2,1 vylepšuje tento pracovní postup díky podpoře aktualizace jako funkce první třídy uživatelského rozhraní konfigurace.

![Dialogové okno Konfigurace Správce balíčků](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Opravy chyb

NuGet 2,1 obsahuje mnoho oprav chyb. Úplný seznam pracovních položek opravených v NuGet 2,0 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
