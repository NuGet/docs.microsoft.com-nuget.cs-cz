---
title: Instalace a správa balíčků NuGet pomocí konzoly v sadě Visual Studio
description: Pokyny pro použití konzoly NuGet Package Manager console v sadě Visual Studio pro práci s balíčky.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 42031f7b5fe4d3c1b4dbe5e1bfbf9197014e0e88
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428952"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>Instalace a správa balíčků pomocí konzoly Správce balíčků v sadě Visual Studio (PowerShell)

Konzola Správce balíčků NuGet umožňuje pomocí [příkazů NuGet PowerShell](../reference/powershell-reference.md) najít, nainstalovat, odinstalovat a aktualizovat balíčky NuGet. Použití konzoly je nezbytné v případech, kdy ui Správce balíčků neposkytuje způsob, jak provést operaci. Informace `nuget.exe` o použití příkazů příkazového příkazu příkazu PŘÍKAZOvého nastavení v konzole naleznete v [tématu Použití příkazového příkazu nuget.exe v konzole](#use-the-nugetexe-cli-in-the-console).

Konzole je integrovándo sady Visual Studio v systému Windows. Není součástí Visual Studio pro Mac nebo Visual Studio kód.

## <a name="find-and-install-a-package"></a>Vyhledání a instalace balíčku

Například nalezení a instalace balíčku se provádí třemi jednoduchými kroky:

1. Otevřete projekt nebo řešení v sadě Visual Studio a otevřete konzolu pomocí **příkazu Nástroje > NuGet Správce balíčků > konzoli správce balíčků.**

1. Najděte balíček, který chcete nainstalovat. Pokud již víte, přejděte ke kroku 3.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Spusťte příkaz instalace:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Všechny operace, které jsou k dispozici v konzole lze provést také s [NuGet CLI](../reference/nuget-exe-cli-reference.md). Příkazy konzoly však pracovat v kontextu sady Visual Studio a uložené projekt/řešení a často dosáhnout více než jejich ekvivalentní příkazy příkazového řádku. Například instalace balíčku prostřednictvím konzoly přidá odkaz na projekt vzhledem k tomu, že příkaz příkazu příkazu příkazu cli nikoli. Z tohoto důvodu vývojáři pracující v sadě Visual Studio obvykle dávají přednost použití konzoly rozhraní cli.

> [!Tip]
> Mnoho operací konzoly závisí na otevření řešení v sadě Visual Studio se známým názvem cesty. Pokud máte neuložené řešení nebo žádné řešení, zobrazí se chyba "Řešení není otevřeno nebo není uloženo. Ujistěte se, že máte otevřené a uložené řešení." To znamená, že konzola nemůže určit složku řešení. Uložení neuloženého řešení nebo vytvoření a uložení řešení, pokud nemáte otevřené, by mělo chybu opravit.

## <a name="opening-the-console-and-console-controls"></a>Otevření ovládacích prvků konzoly a konzoly

1. Otevřete konzolu v sadě Visual Studio pomocí příkazu **Nástroje > Správce balíčků > konzola správce balíčků.** Konzola je okno sady Visual Studio, které lze uspořádat a umístit však chcete (viz [Přizpůsobení rozložení oken v sadě Visual Studio).](/visualstudio/ide/customizing-window-layouts-in-visual-studio)

1. Ve výchozím nastavení konzolové příkazy pracují s určitým zdrojem balíčku a projektem, jak je nastaveno v ovládacím prvku v horní části okna:

    ![Ovládací prvky konzoly Správce balíčků pro zdroj balíčku a projekt](media/PackageManagerConsoleControls1.png)

1. Výběrem jiného zdroje balíčku nebo projektu se změní výchozí hodnoty pro následné příkazy. Chcete-li tato nastavení přepsat bez evidenčních hodnot, podporuje většina příkazů `-Source` a `-ProjectName` možností.

1. Chcete-li spravovat zdroje balíčků, vyberte ikonu ozubeného kola. Toto je zástupce **nástroje > možnosti > NuGet Správce balíčků > zdroje balíčků,** jak je popsáno na stránce [ui Správce balíčků.](install-use-packages-visual-studio.md#package-sources) Ovládací prvek vpravo od voliče projektu také vymaže obsah konzoly:

    ![Nastavení konzoly Správce balíčků a jasné ovládací prvky](media/PackageManagerConsoleControls2.png)

1. Tlačítko zcela vpravo přeruší dlouhotrvající příkaz. Spuštění `Get-Package -ListAvailable -PageSize 500` například uvádí prvních 500 balíčků na výchozím zdroji (například nuget.org), což může trvat několik minut.

    ![Ovládací prvek zastavení konzoly Správce balíčků](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a>Instalace balíčku

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Viz [Instalační balíček](../reference/ps-reference/ps-ref-install-package.md).

Instalace balíčku v konzole provádí stejné kroky, jaké jsou popsány v části [Co se stane při instalaci balíčku](../concepts/package-installation-process.md), s následujícími dodatky:

- Konzola zobrazí příslušné licenční podmínky ve svém okně s předpokládanou smlouvou. Pokud s podmínkami nesouhlasíte, měli byste balíček okamžitě odinstalovat.
- Také odkaz na balíček je přidán do souboru projektu a zobrazí se v **Průzkumníku řešení** v uzlu **Odkazy,** je třeba uložit projekt zobrazíte změny v souboru projektu přímo.

## <a name="uninstall-a-package"></a>Odinstalace balíčku

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Viz [Odinstalovat-Balíček](../reference/ps-reference/ps-ref-uninstall-package.md). Pomocí [get-package](../reference/ps-reference/ps-ref-get-package.md) zobrazíte všechny balíčky aktuálně nainstalované ve výchozím projektu, pokud potřebujete najít identifikátor.

Odinstalování balíčku provede následující akce:

- Odebere odkazy na balíček z projektu (a bez ohledu na formát správy je používán). Odkazy se již nezobrazují v **Průzkumníku řešení**. (Pravděpodobně bude nutné znovu vytvořit projekt, aby byl odebrán ze složky **Bin.)**
- Vrátí všechny změny `app.config` provedené `web.config` v aplikaci nebo při instalaci balíčku.
- Odebere dříve nainstalované závislosti, pokud tyto závislosti nepoužívají žádné zbývající balíčky.

## <a name="update-a-package"></a>Aktualizace balíčku

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

Viz [Get-Package](../reference/ps-reference/ps-ref-get-package.md) a [Update-Package](../reference/ps-reference/ps-ref-update-package.md)

## <a name="find-a-package"></a>Najít balíček

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

Viz [Najít-balíček](../reference/ps-reference/ps-ref-find-package.md). V Sadě Visual Studio 2013 a starší, použijte [get-package](../reference/ps-reference/ps-ref-get-package.md) místo.

## <a name="availability-of-the-console"></a>Dostupnost konzoly

Počínaje Visual Studio 2017 NuGet a NuGet Správce balíčků jsou automaticky nainstalovány, když vyberete libovolné . NET související s úlohami; Můžete jej také nainstalovat jednotlivě kontrolou **jednotlivých součástí > nástroje Code >** možnost i správce balíčků NuGet v instalačním programu sady Visual Studio.

Také pokud chybí Správce balíčků NuGet v sadě Visual Studio 2015 a starší, zkontrolujte **nástroje > rozšíření a aktualizace...** a vyhledejte rozšíření NuGet Package Manager. Pokud se vám nedaří použít instalační program rozšíření v sadě Visual [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)Studio, můžete si rozšíření stáhnout přímo z aplikace .

Konzola Správce balíčků není v současné době k dispozici v sadě Visual Studio for Mac. Ekvivalentní příkazy jsou však k dispozici prostřednictvím [rozhraní příkazového příkazu NuGet](../reference/nuget-exe-CLI-reference.md). Visual Studio pro Mac má ui pro správu balíčků NuGet. Viz [včetně balíčku NuGet v projektu](/visualstudio/mac/nuget-walkthrough).

Konzola Správce balíčků není součástí kódu sady Visual Studio.

## <a name="extend-the-package-manager-console"></a>Rozšíření konzoly Správce balíčků

Některé balíčky instalují nové příkazy pro konzolu. Například `MvcScaffolding` vytvoří příkazy, jako `Scaffold` je uvedeno níže, který generuje ASP.NET MVC řadiče a zobrazení:

![Instalace a používání mvcscaffoldu](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a>Nastavení profilu prostředí NuGet PowerShell

Profil Prostředí PowerShell umožňuje zpřístupnit běžně používané příkazy všude, kde používáte PowerShell. NuGet podporuje profil specifický pro NuGet, který se obvykle nachází v následujícím umístění:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Chcete-li profil `$profile` najít, zadejte do konzole:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Další podrobnosti naleznete v části [Profily prostředí Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="use-the-nugetexe-cli-in-the-console"></a>Použití cli nuget.exe v konzole

Chcete-li [ `nuget.exe` rozhraní příkazového řádku](../reference/nuget-exe-cli-reference.md) zpřístupnit v konzole Správce balíčků, nainstalujte balíček [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) z konzoly:

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
