---
title: Nainstalovat a spravovat balíčky NuGet v sadě Visual Studio pomocí Powershellu
description: Pokyny k používání konzoly Správce balíčků NuGet v sadě Visual Studio pro práci s balíčky.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 11ec25598d3110ba84dec5044642e205e13346af
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426209"
---
# <a name="install-and-manage-packages-using-powershell-in-visual-studio"></a>Instalace a Správa balíčků s využitím prostředí PowerShell v sadě Visual Studio

Konzola správce balíčků NuGet umožňuje používat [příkazy prostředí NuGet PowerShell](../tools/powershell-reference.md) najít, nainstalovat, odinstalujte a aktualizovat balíčky NuGet. Pomocí konzoly je nutné v případech, kdy uživatelské rozhraní Správce balíčků neposkytuje způsob, jak provádět operace. Použití `nuget.exe` příkazy rozhraní příkazového řádku v konzole, najdete v článku [pomocí nuget.exe rozhraní příkazového řádku v konzole](#using-the-nugetexe-cli-in-the-console).

Konzole je součástí sady Visual Studio ve Windows. Není součástí sady Visual Studio pro Mac nebo Visual Studio Code.

## <a name="find-and-install-a-package"></a>Najít a nainstalovat balíček

Vyhledání a instalace balíčku se provádí pomocí tří snadných kroků:

1. Otevřete projekt nebo řešení v sadě Visual Studio a otevřete konzoly pomocí **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkazu.

1. Vyhledání balíčku, který chcete nainstalovat. Pokud již tohle už znáte, pokračujte krokem 3.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Spuštění instalačního příkazu:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Všechny operace, které jsou k dispozici v konzole je možné provést pomocí [rozhraní příkazového řádku NuGet](../tools/nuget-exe-cli-reference.md). Příkazy konzoly však pracovat v rámci sady Visual Studio a uložené projekt nebo řešení a často dosáhnout více než jejich ekvivalentní příkazy rozhraní příkazového řádku. Například při instalaci balíčku prostřednictvím konzoly přidá odkaz na projekt služba nepodporuje příkaz rozhraní příkazového řádku. Z tohoto důvodu vývojáři pracující v sadě Visual Studio obvykle raději pomocí konzoly nástroje rozhraní příkazového řádku.

> [!Tip]
> Mnoho operací konzole závisí na řešení otevřít v sadě Visual Studio s názvem známé cesty. Pokud už máte neuložené řešení nebo žádné řešení, se zobrazí chyba, "řešení není otevřené nebo nebyl uložen. Ujistěte se, že máte řešení otevřené a uložené." To znamená, že konzoly nelze určit složku řešení. Ukládání neuložené řešení, nebo vytvářet a ukládat řešení, pokud ho nemáte otevřete, vyřešte chybu.

## <a name="opening-the-console-and-console-controls"></a>Otevřete konzoly a ovládací prvky konzoly

1. Otevřete konzolu v sadě Visual Studio pomocí **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkazu. Visual Studio okno, které můžete uspořádat a umístěn libovolně je konzola (viz [přizpůsobení rozložení oken v sadě Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Ve výchozím nastavení příkazy konzoly fungovat proti konkrétní balíček zdroje a projekt jako sada v ovládacím prvku v horní části okna:

    ![Ovládací prvky konzoly Správce balíčků pro zdroj balíčku a projektu](media/PackageManagerConsoleControls1.png)

1. Vyberte jiný balíček zdrojové a/nebo projekt se změní tyto výchozí hodnoty pro následné příkazy. Způsobem lze potlačit tato nastavení, aniž byste měnili výchozí hodnoty, většina příkazů podporují `-Source` a `-ProjectName` možnosti.

1. Pokud chcete spravovat zdroje balíčků, vyberte ikonu ozubeného kola. Toto je zástupce **nástroje > Možnosti > Správce balíčků NuGet > zdroje balíčků** dialogovému oknu, jak je popsáno na [uživatelské rozhraní Správce balíčků](package-manager-ui.md#package-sources) stránky. Ovládací prvek vpravo od selektor projektu vymaže obsah v konzole:

    ![Nastavení konzoly Správce balíčků a vymazat ovládacích prvků](media/PackageManagerConsoleControls2.png)

1. Úplně vpravo tlačítko přeruší dlouhotrvající příkazu. Například systém `Get-Package -ListAvailable -PageSize 500` uvádí balíčky horní 500 na výchozí zdroj (jako je nuget.org), což může trvat několik minut.

    ![Ovládací prvek stop Konzola správce balíčků](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Instalace balíčku

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Zobrazit [Install-Package](../tools/ps-ref-install-package.md).

Instalace balíčku v konzole provádí stejným způsobem, jak je popsáno v [co se stane, když je nainstalován balíček](../concepts/package-installation-process.md), s těmito přídavky:

- Této konzole se zobrazují v okně s implicitní dohodu příslušných licenčních podmínkách. Pokud nesouhlasíte s podmínkami, byste měli odinstalovat balíček okamžitě.
- Také odkaz na balíček se přidá do souboru projektu a zobrazí se v **Průzkumníka řešení** pod **odkazy** uzel, je nutné uložit projekt tak, aby se změny v souboru projektu přímo.

## <a name="uninstalling-a-package"></a>Odinstalace balíčku

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Zobrazit [odinstalovat balíček](../tools/ps-ref-uninstall-package.md). Použití [Get-Package](../tools/ps-ref-get-package.md) zobrazíte všechny balíčky, které jsou aktuálně nainstalované ve výchozím projektu, pokud je potřeba najít identifikátor.

Odinstalace balíčku provede následující akce:

- Odebere odkazy na balíček z projektu (a jakékoli formátu správy se používá). Odkazy se už nezobrazují v **Průzkumníka řešení**. (Možná budete muset znovu sestavte projekt a prohlédněte si ho odebrat z **Bin** složky.)
- Obrátí všechny změny provedené `app.config` nebo `web.config` kdy byl nainstalován balíček.
- Odstraní dříve nainstalovali závislosti, pokud žádné zbývající balíčky pomocí těchto závislostí.

## <a name="updating-a-package"></a>Aktualizace balíčku

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

Zobrazit [Get-Package](../tools/ps-ref-get-package.md) a [Update-Package](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>Vyhledání balíčku

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

Zobrazit [najít balíček](../tools/ps-ref-find-package.md). V sadě Visual Studio 2013 a dříve, použít [Get-Package](../tools/ps-ref-get-package.md) místo.

## <a name="availability-of-the-console"></a>Dostupnost konzoly nástroje

Spouští se v sadě Visual Studio 2017, NuGet a Správce balíčků NuGet jsou automaticky nainstalovány se některé vyberte. Úlohy související s NET; můžete ho také nainstalovat jednotlivě kontrolou **jednotlivé komponenty > kód nástroje > Správce balíčků NuGet** možnost v instalačním programu sady Visual Studio.

Zkontrolujte taky, pokud jste chybí Správce balíčků NuGet v sadě Visual Studio 2015 a starší, **nástroje > rozšíření a aktualizace...**  a hledání rozšíření Správce balíčků NuGet. Pokud nemůžete použít instalační program rozšíření v sadě Visual Studio, můžete stáhnout přímo z rozšíření [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).

Konzola správce balíčků není v současné době k dispozici se sadou Visual Studio pro Mac. Ekvivalentní příkazy, ale jsou k dispozici prostřednictvím [rozhraní příkazového řádku NuGet](nuget-exe-CLI-reference.md). Visual Studio pro Mac má uživatelské rozhraní pro správu balíčků NuGet. Zobrazit [balíček včetně NuGet ve vašem projektu](/visualstudio/mac/nuget-walkthrough).

Konzola správce balíčků není součástí systému Visual Studio Code.

## <a name="extending-the-package-manager-console"></a>Rozšíření konzole Správce balíčků

Některé balíčky nainstalovat nové příkazy konzoly. Například `MvcScaffolding` vytvoří příkazů, jako jsou `Scaffold` vidíte níže, která generuje zobrazení a kontrolery ASP.NET MVC:

![Instalace a použití MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Nastavení profilu NuGet Powershellu

Profil PowerShell umožňuje zpřístupnit často používané příkazy bez ohledu na to pomocí prostředí PowerShell. NuGet podporuje NuGet konkrétní profil většinou nacházejí v následujícím umístění:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Chcete-li najít profil, zadejte `$profile` v konzole:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Další podrobnosti najdete v [profily Windows Powershellu](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="using-the-nugetexe-cli-in-the-console"></a>Pomocí nuget.exe rozhraní příkazového řádku v konzole

Aby [ `nuget.exe` rozhraní příkazového řádku](nuget-exe-cli-reference.md) dostupná v konzole Správce balíčků, instalaci [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) balíček z konzoly:

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
