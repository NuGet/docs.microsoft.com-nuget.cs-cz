---
title: Zpráva k vydání verze NuGet 2,8
description: Poznámky k verzi pro NuGet 2,8, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237014"
---
# <a name="nuget-28-release-notes"></a>Zpráva k vydání verze NuGet 2,8

Poznámky k verzi [NuGet 2.7.2](../release-notes/nuget-2.7.2.md)  |  [Poznámky k verzi NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

NuGet 2,8 byl vydán 29. ledna 2014.

## <a name="acknowledgements"></a>Poděkování

1. [Llewellyn Pritcharda](https://www.codeplex.com/site/users/view/leppie) ( [@leppie](https://twitter.com/leppie) )
    - [#3466](https://nuget.codeplex.com/workitem/3466) – při dobalení se ověří ID balíčků závislostí.
2. [Martin Balliauw](https://www.codeplex.com/site/users/view/maartenba) ( [@maartenballiauw](https://twitter.com/maartenballiauw) )
    - [#2379](https://nuget.codeplex.com/workitem/2379) – při přihlašovacích údajích kanálu persistening odebrat příponu $metadata.
3. [Filip de Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ( [@foxtricks](https://twitter.com/foxtricks) )
    - [#3538](http://nuget.codeplex.com/workitem/3538) – podpora určení souboru projektu pro příkaz nuget.exe Update.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - tokeny nahrazení [#3536](http://nuget.codeplex.com/workitem/3536) neprošly parametrem-IncludeReferencedProjects.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ( [@Sarkie_Dave](https://twitter.com/Sarkie_Dave) )
    - [#3677](http://nuget.codeplex.com/workitem/3677) – oprava nugetu. při vložení velkého balíčku se doručí aktivační OutOfMemoryException.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) – oprava nesprávné cílové cesty, pokud se projekt odkazuje na jiný projekt CLI/C++.
7. [Adam petrpo](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - [#3639](https://nuget.codeplex.com/workitem/3639) – povolí instalaci balíčků jako závislostí vývoje ve výchozím nastavení.
8. [David Fowlera](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )
    - [#3717](https://nuget.codeplex.com/workitem/3717) – odebrání implicitních upgradů na nejnovější verzi opravy
9. [Gregoriánský Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Několik oprav chyb a vylepšení pro NuGet. Server, příkaz nuget.exe zrcadlení a další.
    - Tato práce se provedla za několik měsíců, přičemž gregoriánský spolupracuje s námi na správném načasování pro integraci do hlavní větve pro 2,8.

## <a name="patch-resolution-for-dependencies"></a>Řešení opravy pro závislosti

Při vyhodnocování závislostí balíčku NuGet implementovala strategii pro vybírání nejnižší hlavní a dílčí verze balíčku, která splňuje závislosti na balíčku. Na rozdíl od hlavní a dílčí verze však verze opravy vždy přeložila na nejvyšší verzi. I když bylo chování záměrně úmyslné, vytvořilo se nedostatečné determinismem pro instalaci balíčků se závislostmi. Uvažujte následující příklad:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

V tomto příkladu, i když je nainstalovaný Developer1 a Developer2 PackageA@1.0.0 , každá skončila s jinou verzí PackageB. NuGet 2,8 mění toto výchozí chování tak, že chování rozlišení závislosti pro verze patch je konzistentní s chováním pro hlavní a dílčí verze. V předchozím příkladu se pak PackageB@1.0.0 nainstaluje jako výsledek instalace PackageA@1.0.0 bez ohledu na novější verzi patch.

## <a name="-dependencyversion-switch"></a>– Přepínač DependencyVersion

I když NuGet 2,8 mění _výchozí_ chování pro řešení závislostí, přidá taky přesnější kontrolu nad procesem překladu závislostí prostřednictvím přepínače-DependencyVersion v konzole správce balíčků. Přepínač umožňuje překládat závislosti na nejnižší možnou verzi (výchozí chování), nejvyšší možnou verzi nebo nejvyšší dílčí nebo opravnou verzi.  Tento přepínač funguje jenom pro rutinu Install-Package v příkazu PowerShellu.

![Přepínač DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion – atribut

Kromě přepínače-DependencyVersion popsaného výše má NuGet taky možnost nastavit nový atribut v souboru Nuget.Config definujícím výchozí hodnotu, pokud není přepínač-DependencyVersion zadaný při volání Install-Package. Tuto hodnotu bude také respektován dialog správce balíčků NuGet pro všechny operace instalace balíčku. Chcete-li nastavit tuto hodnotu, přidejte následující atribut do souboru Nuget.Config:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Náhled operací NuGet s-whatIf

Některé balíčky NuGet můžou mít hloubkové grafy závislosti a jako takové můžou být užitečné při instalaci, odinstalaci nebo aktualizaci, abyste nejdřív viděli, co se stane. NuGet 2,8 přidá standardní přepínač PowerShellu-whatIf na příkazy Install-Package, Uninstall-Package a Update-Package, aby bylo možné vizualizovat celý uzávěr balíčků, na které se příkaz aplikuje. Například spuštění `install-package Microsoft.AspNet.WebApi -whatif` v prázdné webové aplikaci ASP.NET poskytuje následující.

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

## <a name="downgrade-package"></a>Downgrade – balíček

Není neobvyklé instalovat předprodejní verzi balíčku, aby bylo možné prozkoumat nové funkce a pak se rozhodnout vrátit zpět k poslední stabilní verzi. Před NuGet 2,8 se jednalo o proces odinstalace předprodejního balíčku a jeho závislostí a následná instalace starší verze. S NuGet 2,8 se ale balíček Update-Package vrátí zpátky celý uzávěr balíčku (například strom závislosti balíčku) na předchozí verzi.

## <a name="development-dependencies"></a>Vývojové závislosti

Jako balíčky NuGet se dají doručovat spousty různých typů funkcí – včetně nástrojů, které se používají k optimalizaci procesu vývoje. Tyto komponenty, i když můžou být instrumentované při vývoji nového balíčku, by se při pozdějším publikování neměly považovat za závislost nového balíčku. NuGet 2,8 umožňuje balíčku identifikovat sebe sama v `.nuspec` souboru jako developmentDependency. Po nainstalování budou tato metadata také přidána do `packages.config` souboru projektu, do kterého byl balíček nainstalován. Když `packages.config` se tento soubor později analyzuje pro závislosti NuGet `nuget.exe pack` , vyloučí se tyto závislosti označené jako závislosti na vývoji.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Jednotlivé soubory packages.config pro různé platformy

Při vývoji aplikací pro více cílových platforem je běžné mít různé soubory projektu pro každé z příslušných prostředí sestavení. Také je běžné využívat různé balíčky NuGet v různých souborech projektu, protože balíčky mají různé úrovně podpory pro různé platformy. NuGet 2,8 poskytuje vylepšenou podporu pro tento scénář vytvořením různých `packages.config` souborů pro různé soubory projektu specifické pro platformu.

![Více souborů package.config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Záložní přechod do místní mezipaměti

I když jsou balíčky NuGet typicky spotřebované ze vzdálené galerie, jako [je například galerie NuGet](http://www.nuget.org/) pomocí síťového připojení, existuje mnoho scénářů, ve kterých klient není připojen. Bez připojení k síti klient NuGet nemohl úspěšně nainstalovat balíčky, i když už tyto balíčky na počítači klienta v místní mezipaměti NuGet. NuGet 2,8 přidá do konzoly Správce balíčků automatickou zálohu mezipaměti. Například při odpojení síťového adaptéru a instalaci jQuery konzola nástroje zobrazí následující:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

Funkce Fallback mezipaměti nevyžaduje žádné konkrétní argumenty příkazu. Kromě toho záložní záloha v tuto chvíli funguje jenom v konzole správce balíčků – v dialogovém okně Správce balíčků to chování momentálně nefunguje.

## <a name="webmatrix-nuget-client-updates"></a>Aktualizace klienta NuGet pro WebMatrix

Společně s NuGet 2,8 se rozšíření NuGet pro WebMatrix aktualizovalo taky tak, aby obsahovalo spoustu hlavních funkcí dodaných s [nuget 2,5](../release-notes/nuget-2.5.md). Mezi nové funkce patří například ' Aktualizovat vše ', ' minimální verze NuGet ' a povolit přepisování souborů obsahu.

Aktualizace rozšíření Správce balíčků NuGet ve WebMatrixu 3:

1. Otevřít WebMatrix 3
1. Na pásu karet klikněte na ikonu rozšíření.
1. Vyberte kartu aktualizace.
1. Kliknutím můžete aktualizovat Správce balíčků NuGet na 2.5.0
1. Zavřít a restartovat WebMatrix 3

Toto je první verze rozšíření Správce balíčků NuGet pro WebMatrix v týmu NuGet.  Společnost Microsoft nedávno přispěla do open source projektu NuGet. Dříve byla integrace NuGet integrovaná do WebMatrixu a nepovedlo se jí aktualizovat vzdálenou matrici.  Teď máme možnost je dál aktualizovat vedle zbývajících klientských nástrojů NuGet.

## <a name="bug-fixes"></a>Opravy chyb

Jedna z hlavních oprav chyb způsobila zvýšení výkonu v příkazu Update-Package-REINSTALL.

Kromě těchto funkcí a výše zmíněné opravy výkonu obsahuje tato verze NuGet také mnoho dalších oprav chyb. V této verzi byly vyřešeny 181 celkové problémy. Úplný seznam pracovních položek opravených v NuGet 2,8 najdete v [přehledu problémů NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
