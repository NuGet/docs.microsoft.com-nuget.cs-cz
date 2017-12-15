---
title: "Poznámky k verzi NuGet 2.0 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 51c7e94f-0084-4c62-bfba-7dfd81675361
description: "Poznámky k verzi pro NuGet 2.0 včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 2.0 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 41eed1a7c6ad91d63813fb74986aa498765f3dea
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-20-release-notes"></a>Poznámky k verzi 2.0 NuGet

[Poznámky k verzi NuGet 1.8](../release-notes/nuget-1.8.md) | [NuGet 2.1 poznámky k verzi](../release-notes/nuget-2.1.md)

NuGet 2.0 byla vydána 19. června 2012.

## <a name="known-installation-issue"></a>Instalace známý problém
Pokud používáte VS 2010 SP1, můžete spustit došlo k chybě instalace při pokusu o upgrade NuGet, pokud máte nainstalovaný starší verze.

Alternativní řešení je jednoduše odinstalovat NuGet a nainstalujte ji z Galerie rozšíření VS.  V tématu [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) Další informace, nebo [přejděte přímo na opravu hotfix VS](http://bit.ly/vsixcertfix).

Poznámka: Pokud Visual Studio nebude možné odinstalovat rozšíření (k dispozici tlačítko Odinstalovat), bude pravděpodobně nutné restartujte Visual Studio pomocí "Spustit jako správce."

## <a name="package-restore-consent-is-now-active"></a>Balíček souhlasu obnovení je teď aktivní

Jak je popsáno v tomto [můžete zveřejnit na balíček obnovení souhlasu](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 nyní vyžadují souhlasu umožňující obnovení balíčků přejděte do režimu online a stáhnout balíčky. Zkontrolujte, zda jste zadali souhlasu prostřednictvím dialogu konfigurace správce balíčku nebo proměnné prostředí EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Závislosti skupiny podle cílové rozhraní

Od verze 2.0, balíčku, který se může lišit v závislosti na základě framework profilu cíl projektu. Toho dosahuje pomocí aktualizované `.nuspec` schématu. `<dependencies>` Element může obsahovat teď sadu `<group>` elementy. Každá skupina obsahuje nula nebo více `<dependency>` elementy a `targetFramework` atribut. Pokud cílovém Frameworku, který je kompatibilní s profilem cílový framework projektu byly společně nainstalované všechny závislosti uvnitř skupiny. Příklad:

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

Všimněte si, že skupina může obsahovat **nula** závislosti. V příkladu nahoře Pokud tento balíček je nainstalovaný do projektu, jehož cílem Silverlight 3.0 nebo novější, nemá žádné závislosti budou nainstalovány. Pokud balíček je nainstalovaný do projektu, jehož cílem rozhraní .NET 4.0 nebo novější, obě závislosti, jQuery a WebActivator, budou nainstalovány.  Pokud instalaci balíčku do projektu, jehož cílem starší verzí tyto 2 architektury nebo jiných framework RouteMagic 1.1.0 se nainstaluje. Neexistuje žádné dědičnosti mezi skupinami. Pokud cílový framework projektu na odpovídá `targetFramework` nainstaluje atribut skupiny jenom závislosti v rámci dané skupiny.

Balíček můžete určit závislosti balíčků v některém z dva formáty: starý formát plochý seznam `<dependency>` elementy nebo skupiny. Pokud `<group>` použít formát, balíček nelze nainstalovat do verze NuGet starší než 2.0.

Všimněte si, že kombinování dvěma formáty není povolené. Například následující fragment kódu je **neplatný** a budou odmítnuty systémem NuGet.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Seskupování podle cílové rozhraní soubory obsahu a skriptů prostředí PowerShell

Kromě odkazy na sestavení soubory obsahu a skriptů prostředí PowerShell můžete taky Seskupit podle cílové rozhraní. Stejnou strukturu složek najít v `lib` složku pro zadání cílové rozhraní je nyní možné použít v stejným způsobem, jako `content` a `tools` složek. Příklad:

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

**Poznámka:**: protože `init.ps1` je proveden na úrovni řešení a není závislá na všech jednotlivých projektů, je nutné ji umístit přímo pod `tools` složky. Pokud se umístit do složky pro konkrétní rozhraní, se budou ignorovat.

Novou funkcí systému NuGet 2.0 je také, že lze složku rozhraní *prázdný*, v takovém případě nebude přidejte odkazy na sestavení, přidání souborů obsahu nebo spuštění skriptů prostředí PowerShell pro konkrétní verzi NuGet. V příkladu výše, složce `content\net40` je prázdný.

## <a name="improved-tab-completion-performance"></a>Vylepšené karta dokončení výkonu
Funkci karta dokončení v konzole Správce balíčků NuGet se aktualizovalo a výrazně zlepšit výkon. Bude mnohem menší zpoždění od okamžiku, kdy stisknutí klávesy tab, až se zobrazí rozevírací seznam návrhu.

## <a name="bug-fixes"></a>Opravy chyb
NuGet 2.0 zahrnuje mnoho opravy chyb s důrazem na balíček obnovení souhlasu a výkonu.
Úplný seznam pracovní položky pevná ve NuGet 2.0, prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
