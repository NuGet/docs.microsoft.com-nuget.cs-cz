---
title: Zpráva k vydání verze NuGet 2,0
description: Poznámky k verzi pro NuGet 2,0, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6874cbf0404f18ab7007bec1e0f66089c790d08
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776992"
---
# <a name="nuget-20-release-notes"></a>Zpráva k vydání verze NuGet 2,0

Zpráva k [vydání verze](../release-notes/nuget-1.8.md)  |  NuGet 1,8 Zpráva k [vydání verze NuGet 2,1](../release-notes/nuget-2.1.md)

NuGet 2,0 byl vydán 19. června 2012.

## <a name="known-installation-issue"></a>Známý problém s instalací
Pokud používáte VS 2010 SP1, můžete při pokusu o upgrade NuGetu v případě, že máte nainstalovanou starší verzi, spustit chybu instalace.

Alternativním řešením je jednoduše odinstalovat NuGet a pak ji nainstalovat z galerie rozšíření VS.  Další informace najdete v tématu <https://support.microsoft.com/kb/2581019> , kde najdete další informace, nebo [přejděte přímo na opravu hotfix vs](http://bit.ly/vsixcertfix).

Poznámka: Pokud Visual Studio neumožní odinstalovat rozšíření (tlačítko Odinstalace je zakázané), pak budete pravděpodobně muset restartovat Visual Studio pomocí možnosti Spustit jako správce.

## <a name="package-restore-consent-is-now-active"></a>Souhlasu balíčku pro obnovení je teď aktivní.

Jak je popsáno v tomto [příspěvku o souhlasu s obnovením balíčku](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2,0 nyní vyžaduje souhlas s povolením, aby obnovení balíčků mohlo přejít online a stáhnout balíčky. Ujistěte se prosím, že jste poskytli souhlas prostřednictvím dialogu konfigurace správce balíčků nebo proměnné prostředí EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Seskupení závislostí podle cílových rozhraní

Počínaje verzí 2,0 se závislosti balíčků můžou lišit v závislosti na profilu rozhraní cílového projektu. To je provedeno pomocí aktualizovaného `.nuspec` schématu. `<dependencies>`Element může nyní obsahovat sadu `<group>` prvků. Každá skupina obsahuje nula nebo více `<dependency>` elementů a `targetFramework` atribut. Všechny závislosti v rámci skupiny jsou nainstalovány společně, pokud je cílový rámec kompatibilní s profilem cílového projektového architektury. Například:

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

Všimněte si, že skupina může obsahovat **nulové** závislosti. Pokud se v předchozím příkladu nainstaluje balíček do projektu, který cílí na Silverlight 3,0 nebo novější, nebudou nainstalovány žádné závislosti. Pokud je balíček nainstalován do projektu cíleného na rozhraní .NET 4,0 nebo novější, budou nainstalovány dvě závislosti, jQuery a webactivator.  Pokud se balíček nainstaluje do projektu, který se zaměřuje na počáteční verzi těchto 2 platforem, nebo na jakékoli jiné rozhraní, nainstaluje se RouteMagic 1.1.0. Mezi skupinami neexistuje žádná dědičnost. Pokud cílové rozhraní projektu odpovídá `targetFramework` atributu skupiny, budou nainstalovány pouze závislosti v této skupině.

Balíček může určovat závislosti balíčků v jednom ze dvou formátů: ve starém formátu nestrukturovaného seznamu `<dependency>` prvků nebo skupin. Při `<group>` použití formátu se balíček nedá nainstalovat do verzí NuGet starších než 2,0.

Všimněte si, že kombinace těchto dvou formátů není povolená. Například následující fragment kódu je **neplatný** a bude NuGet odmítnut.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Seskupení souborů obsahu a skriptů PowerShellu podle cílové architektury

Kromě odkazů na sestavení je také možné seskupit soubory obsahu a skripty prostředí PowerShell podle cílové architektury. Stejná struktura složek, která se nachází ve `lib` složce pro určení cílové architektury, se teď dá použít stejným způsobem jako `content` složky a `tools` . Například:

```
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
```

**Poznámka**: vzhledem k tomu `init.ps1` , že je provedena na úrovni řešení a není závislý na žádném jednotlivém projektu, musí být přímo pod `tools` složkou. Pokud je umístěn do složky specifické pro rozhraní, bude ignorováno.

Nová funkce v NuGet 2,0 je taky to, že složka rozhraní může být *prázdná*. v takovém případě NuGet nepřidá odkazy na sestavení, přidá soubory obsahu nebo spustí skripty PowerShellu pro konkrétní verzi Frameworku. Ve výše uvedeném příkladu `content\net40` je složka prázdná.

## <a name="improved-tab-completion-performance"></a>Vylepšený výkon dokončování karet
Funkce dokončování karet v konzole správce balíčků NuGet se aktualizovala tak, aby významně zvýšila výkon. Čas stisknutí klávesy TAB bude mnohem kratší, dokud se nezobrazí rozevírací seznam návrh.

## <a name="bug-fixes"></a>Opravy chyb
NuGet 2,0 obsahuje mnoho oprav chyb s důrazem na dodržování souhlasu a výkonu balíčku pro obnovení.
Úplný seznam pracovních položek opravených v NuGet 2,0 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
