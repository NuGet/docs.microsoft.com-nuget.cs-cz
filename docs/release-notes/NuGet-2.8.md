---
title: Poznámky k verzi 2,8 NuGet
description: Poznámky k verzi pro NuGet 2.8 včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f472f1370bfedaf04ebe889c0da01155b8aec22
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2018
ms.locfileid: "32044687"
---
# <a name="nuget-28-release-notes"></a>Poznámky k verzi 2,8 NuGet

[Poznámky k verzi NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 poznámky k verzi](../release-notes/nuget-2.8.1.md)

NuGet 2.8 byla vydána 29. ledna 2014.

## <a name="acknowledgements"></a>Potvrzení

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) – pokud balení balíčky, ověření Id závislostí balíčků.
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -odebrat příponu $metadata při persistening kanálu přihlašovací údaje.
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) – podpora zadání příkazu update nuget.exe souboru projektu.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -není dokončena s - IncludeReferencedProjects tokeny nahrazení.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -opravte nuget.push vyvolání OutOfMemoryException při nabízení velký balíček.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -oprava nesprávné cílová cesta při projekt odkazuje na jiný projekt rozhraní příkazového řádku/C++.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -povolit balíčky určené k instalaci jako závislosti vývoj ve výchozím nastavení
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -odebrat implicitní upgrade na nejnovější verzi opravy
9. [DaN Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Několik chyb, opravy a vylepšení pro NuGet.Server, příkaz nuget.exe zrcadlení a dalších.
    - Tento pracovní bylo provedeno za několik měsíců, s daN na v pravém načasování integrovat do správce pro 2.8.

## <a name="patch-resolution-for-dependencies"></a>Řešení opravy pro závislosti

Při rozpoznávání závislosti balíčků, NuGet v minulosti implementovala strategie výběru nejnižší verze hlavní a podverze balíčku, který splňuje požadavky závislosti na balíčku. Na rozdíl od hlavní a vedlejší verzi ale oprav verze vždy vyřešila nejvyšší verze. I když byl úmyslného chování, vytvořit chybějících determinism pro instalaci balíčků se závislostmi. Podívejte se na následující příklad:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

V tomto příkladu, i když Developer1 a Developer2 nainstalovány PackageA@1.0.0, až se každý zakončeno s jinou verzi PackageB. NuGet 2.8 změní toto výchozí chování tak, aby byla konzistentní s chování pro hlavní verze a podverze chování řešení závislostí pro verze opravy. V předchozím příkladu, pak PackageB@1.0.0 by být nainstalován v důsledku instalace PackageA@1.0.0bez ohledu novější verzi opravy.

## <a name="-dependencyversion-switch"></a>DependencyVersion – přepínač

Když se změní NuGet 2.8 _výchozí_ chování pro řešení závislostí, přidá také přesnější kontrolu nad závislost procesu překladu, který prostřednictvím přepínačem - DependencyVersion v konzole Správce balíčků. Přepínač umožňuje řešení závislosti na nejnižší možné verze (výchozí nastavení), nejvyšší možné verze nejvyšší menší nebo verzi opravy.  Tento přepínač funguje pouze pro instalaci balíčku v příkaz prostředí powershell.

![DependencyVersion přepínače](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Atribut DependencyVersion

Kromě přepínačem - DependencyVersion popsané výše, NuGet má také povolené pro možnost nastavit nový atribut v souboru Nuget.Config definování co výchozí hodnota je, pokud přepínačem - DependencyVersion není zadané v k vyvolání instalace balíčku. Tato hodnota musejí být dodržovány také pomocí dialogového okna Správce balíčků NuGet pro všechny operace instalace balíčku. Pokud chcete nastavit tuto hodnotu, do souboru Nuget.Config přidáte atribut níže:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Operace NuGet Preview s - whatif

Některé balíčky NuGet může mít grafy hloubkové závislostí a jako takový ho může být užitečné při instalaci, odinstalovat nebo aktualizovat operace nejprve zobrazit, co se stane. NuGet 2.8 přidá standardní přepínač - whatif prostředí PowerShell install-package, odinstalujte balíčku a balíček aktualizace příkazy Povolit vizualizace celý uzavření balíčky, pro které bude použito příkaz. Například běžet `install-package Microsoft.AspNet.WebApi -whatif` v prázdný ASP.NET Web application vypočítá následující.

    PM> install-package Microsoft.AspNet.WebApi -whatif
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
    Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
    Install Newtonsoft.Json 4.5.11
    Install Microsoft.AspNet.WebApi.Client 5.0.0
    Install Microsoft.AspNet.WebApi.Core 5.0.0
    Install Microsoft.AspNet.WebApi.WebHost 5.0.0
    Install Microsoft.AspNet.WebApi 5.0.0

## <a name="downgrade-package"></a>Přechod na starší verzi balíčku

Není-li prozkoumat nové funkce, nainstalujte předprodejní verze balíčku a rozhodněte, pak se vrátit zpět poslední stabilní verze neobvyklé. Před NuGet 2.8 šlo vícekrokový proces odinstalace předprodejní balíček a jeho závislosti a následnou instalaci starší verze. S 2.8 NuGet ale balíčku aktualizace bude nyní vrátit zpět uzavření celého balíčku (například strom závislosti balíčku) na předchozí verzi.

## <a name="development-dependencies"></a>Vývoj pro závislosti

Mnoho různých typů možnosti mohou být zajišťovány jako balíčky NuGet - včetně nástrojů, které se používají pro optimalizaci procesu vývoje. Tyto součásti, zatímco můžou být instrumentálního při vývoji nový balíček, by se neměla považovat závislost nového balíčku při později publikování. NuGet 2.8 umožňuje balíček identifikovat v `.nuspec` souboru jako developmentDependency. Při instalaci, tato metadata se dá přidat taky do `packages.config` souboru projektu, do kterého byl nainstalován balíček. Když, `packages.config` později NuGet závislosti během analýzy souboru `nuget.exe pack`, vyloučí těchto závislostí označen jako vývoj závislosti.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Soubor packages.config jednotlivé soubory pro různé platformy

Při vývoji aplikací pro více cílových platforem, se běžně používají různé soubory projektu pro každou z prostředí příslušných sestavení. Je také běžné využívají různé balíčků NuGet v souborech jiný projekt, jak balíčky mají různé úrovně podpory pro různé platformy. NuGet 2.8 poskytuje lepší podporu pro tento scénář vytvořením různých `packages.config` souborů pro soubory jiný projekt specifické pro platformu.

![Více souborů package.config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Přechod na místní mezipaměti

I když z Galerie vzdálené balíčky NuGet obvykle využívat jako [Galerie NuGet](http://www.nuget.org/) použití síťového připojení, existuje mnoho scénářů, kde klient není připojen. Bez připojení k síti nebylo možno k úspěšné instalaci balíčků - i v případě, že tyto balíčky již byly v počítači klienta v místní mezipaměti NuGet klienta NuGet. NuGet 2.8 mezipaměť automatické záložní přidá do konzoly Správce balíčků. Například při odpojení síťového adaptéru a instalujete jQuery, se konzola zobrazí následující:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

Záložní funkci mezipaměti nevyžaduje žádné argumenty konkrétní příkaz. Kromě toho záložní ukládání do mezipaměti aktuálně funguje pouze v konzole Správce balíčků – chování momentálně nefunguje v dialogové okno Správce balíčků.

## <a name="webmatrix-nuget-client-updates"></a>Aktualizace klienta NuGet službu WebMatrix

Společně s NuGet 2.8 rozšíření NuGet pro službu WebMatrix bylo rovněž aktualizováno mnoho dodaná s hlavní funkcí [NuGet 2.5](../release-notes/nuget-2.5.md). Nové funkce patří například aktualizovat vše, 'minimální verze NuGet a povolení pro přepsání souborů obsahu.

Aktualizace rozšíření Správce balíčků NuGet v WebMatrix 3:

1. Otevřete službu WebMatrix 3
1. Klikněte na ikonu rozšíření na pásu karet
1. Vyberte kartu aktualizace
1. Klikněte na tlačítko Aktualizovat na 2.5.0 Správce balíčků NuGet
1. Zavřete a znovu spusťte službu WebMatrix 3

Toto je první verze NuGet team rozšíření Správce balíčků NuGet pro službu WebMatrix.  Kód byl nedávno přispěl Microsoft, do projektu NuGet open source. Dříve integraci NuGet bylo vytvořeno do služby WebMatrix a nebylo možné aktualizovat vzdáleně ze služby WebMatrix.  Nyní je k dispozici možnost Další jej aktualizovat společně se zbytek nástrojích klienta NuGet.

## <a name="bug-fixes"></a>Opravy chyb

Jedním z hlavních opravy chyb provedené byl zlepšování výkonu v balíčku aktualizace-přeinstalujte příkaz.

Kromě těchto funkcí a opravte zmíněnými výkonu tato verze NuGet také obsahuje mnoho ostatní opravy chyb. Nebyly 181 celkový problémy řešeny v verze. Úplný seznam pracovní položky pevná ve NuGet 2.8 prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
