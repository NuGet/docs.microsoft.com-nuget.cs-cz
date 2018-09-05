---
title: Zpráva k vydání 2.8 verze NuGet
description: Zpráva k vydání verze pro NuGet 2.8 včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547456"
---
# <a name="nuget-28-release-notes"></a>Zpráva k vydání 2.8 verze NuGet

[Zpráva k vydání verze NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [zpráva k vydání verze NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

NuGet 2.8 byla vydána 29. ledna 2014.

## <a name="acknowledgements"></a>Potvrzení

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) – při balení balíčky, ověření Id závislosti balíčků.
2. [Martin Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) – odeberte příponu $metadata při persistening informačního kanálu přihlašovací údaje.
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) – podpora zadávání soubor projektu pro příkaz update nuget.exe.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -nebyl předán s - IncludeReferencedProjects tokeny nahrazení.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) – oprava nuget.push vyvolání OutOfMemoryException při odesílání velkých balíčků.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) – oprava nesprávné cílovou cestu, když projekt odkazuje na jiný projekt rozhraní příkazového řádku/C++.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -povolit balíčky, které mají být ve výchozím nastavení nainstalovaná jako vývoj závislosti
8. [David Fowlera](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -odebrat implicitní aktualizován na nejnovější verzi opravy
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Některé opravy chyb a vylepšení pro NuGet.Server, příkaz nuget.exe zrcadlení a další.
    - Tato práce bylo provedeno na několik měsíců, s Gregory práce s námi o správné časování pro integraci do hlavní větve pro 2.8.

## <a name="patch-resolution-for-dependencies"></a>Řešení opravy pro závislosti

Při překladu závislosti balíčků NuGet v minulosti implementoval strategie výběr nejnižší verze hlavní a dílčí balíček, který splňuje požadavky závislosti na balíčku. Na rozdíl od hlavní a dílčí verze ale verze opravy vždy přeložila na nejvyšší verzi. I když byla úmyslného chování, vytvoří nedostatku determinismus pro instalaci balíčků se závislostmi. Vezměte v úvahu v následujícím příkladu:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

V tomto příkladu, i když Developer1 Developer2 nainstalovány a PackageA@1.0.0, každý zakončeno nahoru s jinou verzí PackageB. NuGet 2.8 změní toto výchozí chování tak, aby chování řešení závislostí pro opravu verze je v souladu s chování pro hlavní verze a podverze. V příkladu výše, pak PackageB@1.0.0 by se nainstaloval v důsledku instalaci PackageA@1.0.0bez ohledu novější verzi opravy.

## <a name="-dependencyversion-switch"></a>DependencyVersion – přepínač

Když se změní NuGet 2.8 _výchozí_ chování pro vyřešení závislostí, také přidá přesnější kontrolu nad procesem řešení závislostí prostřednictvím přepínače - DependencyVersion v konzole Správce balíčků. Přepínač umožňuje řešení závislostí na nejnižší možné verze (výchozí chování), nejvyšší možné verzi, nebo nejvyšší podverze nebo verzi opravy.  Tento přepínač funguje jenom pro install-package v příkazu prostředí powershell.

![DependencyVersion přepínače](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Atribut DependencyVersion

Kromě přepínačem - DependencyVersion výše popsané, NuGet je také povolena pro možnost nastavit nový atribut v souboru Nuget.Config definování co je výchozí hodnota, pokud není zadán přepínač - DependencyVersion v vyvolání Install-package. Tato hodnota se také budou dodržovat i dialogové okno Správce balíčků NuGet pro všechny operace instalace balíčku. Nastavení této hodnoty, přidejte do souboru Nuget.Config atribut níže:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Operace NuGet ve verzi Preview s - whatif

Některé balíčky NuGet může mít hloubkové závislosti grafy, a v důsledku toho může být užitečné při instalaci, odinstalovat nebo aktualizovat operace nejprve naleznete v tématu co se stane. NuGet 2.8 přidá standardní přepínač - whatif Powershellu install-package, odinstalovat balíček a vizualizaci celého uzavření balíčky, na které se použije příkaz příkazy update-package. Například systém `install-package Microsoft.AspNet.WebApi -whatif` v prázdný Web ASP.NET aplikace provede následující.

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

Není, chcete-li nainstalovat zkušební verzi balíčku, aby prozkoumat nové funkce a potom se rozhodnete vrátit zpět poslední stabilní verzi. Před 2.8 NuGet to bylo vícefázový proces odinstalace předprodejní balíček a jeho závislosti a následná instalace předchozí verzi. S NuGet 2.8 však balíčku aktualizace bude nyní vrátit zpět uzavření celého balíčku (například strom závislostí balíčku) k předchozí verzi.

## <a name="development-dependencies"></a>Vývoj pro závislosti

Mnoho různých typů funkcí můžete dodávány jako balíčky NuGet – včetně nástrojů, které se používají pro optimalizaci procesu vývoje. Tyto komponenty, zatímco mohou být přispěly k vývoji nového balíčku, by neměly být zahrnuté závislost nového balíčku později publikovaného. NuGet 2.8 umožňuje balíček identifikovat v `.nuspec` soubor jako developmentDependency. Při instalaci těchto metadat se také zařadí do `packages.config` souboru projektu, do kterého byl nainstalován balíček. Když, který `packages.config` souboru je později analyzován z hlediska závislostí NuGet během `nuget.exe pack`, dojde k vyloučení těchto závislostí, označen jako vývoj závislosti.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Soubor packages.config jednotlivých souborů pro různé platformy

Při vývoji aplikací pro více cílových platforem, je běžné mít různé soubory projektu pro každé prostředí příslušné sestavení. Je také běžné využívání různých balíčků NuGet v různé soubory projektu, jak balíčky mají různé úrovně podpory pro různé platformy. NuGet 2.8 poskytuje vylepšenou podporu pro tento scénář tak, že vytvoříte různé `packages.config` souborů pro soubory jiného projektu pro konkrétní platformu.

![Více souborů package.config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Použití náhradní lokality do místní mezipaměti

I když balíčky NuGet jsou obvykle spotřebované vzdálené Galerie jako [Galerie NuGet](http://www.nuget.org/) pomocí připojení k síti, existuje mnoho scénářů, ve kterém není klient připojen. Bez připojení k síti nebylo možné úspěšně nainstalovat balíčky – i v případě, že již byly tyto balíčky na klientském počítači v místní mezipaměti NuGet klienta NuGet. NuGet 2.8 mezipaměť automatické použití náhradní lokality přidá do konzoly Správce balíčků. Například když odpojení síťového adaptéru a instalujete jQuery, konzoly se zobrazí následující:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

Náhradní funkce mezipaměti nevyžaduje žádné argumenty konkrétní příkaz. Kromě toho mezipaměti použití náhradní lokality v současné době používá jenom v konzole Správce balíčků – chování aktuálně nefunguje v dialogové okno Správce balíčků.

## <a name="webmatrix-nuget-client-updates"></a>Aktualizace služby WebMatrix pro klienta NuGet

Spolu s NuGet 2.8 rozšíření NuGet pro službu WebMatrix bylo rovněž aktualizováno řadu hlavní funkce dodávají s [NuGet 2.5](../release-notes/nuget-2.5.md). Mezi nové schopnosti patří těch, jako je například aktualizovat vše 'minimální verze NuGet"a umožňuje přepsání souborů obsahu.

Aktualizace rozšíření Správce balíčků NuGet ve službě WebMatrix 3:

1. Otevřete nástroj WebMatrix 3
1. Klikněte na ikonu rozšíření na pásu karet
1. Vyberte kartu aktualizace
1. Klikněte na tlačítko Aktualizovat na 2.5.0 Správce balíčků NuGet
1. Zavřete a znovu spusťte službu WebMatrix 3

Toto je první verze NuGet týmu rozšíření Správce balíčků NuGet pro službu WebMatrix.  Kód byl nedávno přispěl Microsoft, do projektu NuGet open source. Dříve integrace NuGet se integrovaná do služby WebMatrix a nebylo možné aktualizovat vzdáleně ze služby WebMatrix.  Nyní je k dispozici možnost dál aktualizovat společně s rest klientských nástrojů Nugetu.

## <a name="bug-fixes"></a>Opravy chyb

Byl jeden ze hlavní opravy provedli zlepšování výkonu v balíčku aktualizace-přeinstalujte příkazu.

Kromě těchto funkcí a opravte výše uvedené výkonu tato verze NuGet obsahuje také mnoho ostatní opravy chyb. Došlo k 181 celkový problémy zákazníky a vyřešené ve verzi. Úplný seznam pracovní položky opravených NuGet 2.8 prosím zobrazení [NuGet sledování problémů pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
