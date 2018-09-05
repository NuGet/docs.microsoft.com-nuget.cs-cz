---
title: Poznámky k verzi 2.0 NuGet
description: Zpráva k vydání verze NuGet 2.0, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547572"
---
# <a name="nuget-20-release-notes"></a>Poznámky k verzi 2.0 NuGet

[Zpráva k vydání verze NuGet 1.8](../release-notes/nuget-1.8.md) | [zpráva k vydání verze NuGet 2.1](../release-notes/nuget-2.1.md)

NuGet 2.0 vydané 19. června 2012.

## <a name="known-installation-issue"></a>Instalace známý problém
Pokud spustíte VS 2010 SP1, můžete narazit na chybu instalace při pokusu o upgradu Nugetu, pokud máte nainstalovaný starší verze.

Alternativním řešením je jednoduše odinstalovat NuGet a nainstalujte ho z Galerie rozšíření VS.  Zobrazit [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Další informace nebo [přejděte přímo na opravu hotfix VS](http://bit.ly/vsixcertfix).

Poznámka: Pokud Visual Studio neumožní odinstalovat rozšíření (tlačítko Odinstalovat je vypnutá), pak pravděpodobně nutné restartovat Visual Studio pomocí příkazu "Spustit jako správce."

## <a name="package-restore-consent-is-now-active"></a>Souhlas obnovení balíčku je teď aktivní

Jak je popsáno v tomto [Zveřejněte na souhlas obnovení balíčku](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 bude nyní vyžadovat souhlasu povolit obnovení balíčků přejít online a stáhnout balíčky. Ujistěte se prosím, že jste zadali souhlasu prostřednictvím dialogu konfigurace Správce balíčků nebo proměnné prostředí EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Skupina závislostí podle cílových platforem

Od verze 2.0, balíček, který se může lišit v závislosti na základě v rámci profilu na cílový projekt. To lze provést pomocí aktualizovaného `.nuspec` schématu. `<dependencies>` Element teď může obsahovat sadu `<group>` elementy. Každá skupina obsahuje nula nebo více `<dependency>` elementy a `targetFramework` atribut. Pokud cílová architektura, která je kompatibilní s profil cílového rozhraní framework projektu, jsou všechny závislosti uvnitř skupiny nainstalovaných společně. Příklad:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

Všimněte si, že skupina může obsahovat **nula** závislosti. V předchozím příkladu Pokud je balíček nainstalován do projektu, který cílí na technologii Silverlight 3.0 nebo novější, nemá žádné závislosti se nainstaluje. Pokud balíček je nainstalovaný do projektu, který cílí na rozhraní .NET 4.0 nebo novější, dvě závislosti, jQuery a WebActivator, se nainstalují.  Pokud je balíček nainstalován do projektu, který cílí na starší verzi aplikace tyto 2 architektury nebo libovolné jiné architektury, nainstaluje se RouteMagic 1.1.0. Neexistuje žádné dědičnosti mezi skupinami. Pokud cílové rozhraní projektu odpovídá `targetFramework` atribut skupiny, jenom závislosti v rámci této skupiny se nainstaluje.

Balíček můžete určit závislosti balíčků v některém z dva formáty: starý formát plochý seznam `<dependency>` elementy nebo skupiny. Pokud `<group>` formát se používá, balíček nejde nainstalovat do verze NuGet starší než 2.0.

Všimněte si, že míchání dva formáty nejsou povolené. Například následující fragment kódu je **neplatný** a odmítne NuGet.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Seskupení obsahu soubory a skripty prostředí PowerShell pomocí rozhraní .NET framework

Kromě odkazů na sestavení soubory obsahu a skripty prostředí PowerShell můžete taky Seskupit podle cílovou architekturu. Součástí stejné struktury složek `lib` složku pro zadání cílové rozhraní se teď může používat stejně jako na `content` a `tools` složek. Příklad:

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

**Poznámka:**: protože `init.ps1` provádí na úrovni řešení a není závislá na každý individuální projekt, se musí umístit přímo pod `tools` složky. Pokud umístěné ve složce pro konkrétní rozhraní, bude se ignorovat.

Nová funkce ve verzi NuGet 2.0 je také, že framework složka může představovat *prázdný*, v takovém případě nebude přidat odkazy na sestavení, přidání souborů obsahu nebo spouštění skriptů prostředí PowerShell pro konkrétní framework verze NuGet. V příkladu výše, složce `content\net40` je prázdný.

## <a name="improved-tab-completion-performance"></a>Vylepšené kartu dokončení výkonu
Aktualizovali jsme funkci doplňování kartu v konzole Správce balíčků NuGet k výraznému zlepšení výkonu. Bude mnohem menším zpoždění od okamžiku, kdy stisknutí klávesy tab, dokud se zobrazí rozevírací seznam návrhů.

## <a name="bug-fixes"></a>Opravy chyb
NuGet 2.0 obsahuje řadu oprav chyb s důrazem na souhlas obnovení balíčků a výkon.
Úplný seznam pracovních položek opravených NuGet 2.0 prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
