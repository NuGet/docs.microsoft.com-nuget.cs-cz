---
title: Instalace a Správa balíčků NuGet pomocí konzoly nástroje v aplikaci Visual Studio
description: Pokyny k použití konzoly Správce balíčků NuGet v aplikaci Visual Studio pro práci s balíčky.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 31fa51bc017eaaf9306d5f267e5d4b0d7a15ec9c
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699835"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>Instalace a Správa balíčků pomocí konzoly Správce balíčků v aplikaci Visual Studio (PowerShell)

Konzola správce balíčků NuGet umožňuje používat [příkazy NuGet PowerShellu](../reference/powershell-reference.md) k vyhledání, instalaci, odinstalaci a aktualizaci balíčků NuGet. V případech, kdy uživatelské rozhraní Správce balíčků neposkytuje způsob provedení operace, je nutné použít konzolu. Chcete-li použít `nuget.exe` příkazy rozhraní příkazového řádku v konzole nástroje, přečtěte si téma [použití nuget.exe CLI v konzole](#use-the-nugetexe-cli-in-the-console).

Konzola je integrována do sady Visual Studio ve Windows. Není součástí Visual Studio pro Mac ani Visual Studio Code.

> [!Important]
> Níže uvedené příkazy jsou specifické pro konzolu Správce balíčků v aplikaci Visual Studio a liší se od [příkazů modulu Správa balíčků](/powershell/module/packagemanagement/) , které jsou k dispozici v obecném prostředí PowerShell. Konkrétně každé prostředí obsahuje příkazy, které nejsou k dispozici v druhém a příkazy se stejným názvem se mohou v jejich specifických argumentech také lišit. Při použití konzoly Správa balíčků v aplikaci Visual Studio platí příkazy a argumenty popsané v tomto stávajícím tématu.

## <a name="find-and-install-a-package"></a>Vyhledání a instalace balíčku

Například vyhledání a instalace balíčku se provádí pomocí tří snadných kroků:

1. Otevřete projekt nebo řešení v aplikaci Visual Studio a otevřete konzolu pomocí **nástrojů > správce balíčků NuGet > příkaz konzoly Správce balíčků** .

1. Najděte balíček, který chcete nainstalovat. Pokud už to znáte, přejděte ke kroku 3.

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
> Všechny operace, které jsou k dispozici v konzole nástroje, lze také provést pomocí rozhraní příkazového [řádku NuGet](../reference/nuget-exe-cli-reference.md). Nicméně příkazy konzoly fungují v kontextu aplikace Visual Studio a uloženého projektu nebo řešení a často doplní více než ekvivalentní příkazy rozhraní příkazového řádku. Například instalace balíčku prostřednictvím konzoly přidá odkaz na projekt, zatímco příkaz CLI neprovede. Z tohoto důvodu vývojáři pracující v aplikaci Visual Studio obvykle upřednostňují použití konzoly pro rozhraní příkazového řádku.

> [!Tip]
> Mnoho operací konzoly závisí na tom, že se řešení otevřelo v aplikaci Visual Studio se známým názvem cesty. Pokud máte neuložené řešení nebo žádné řešení, zobrazí se tato chyba: řešení není otevřeno nebo není uloženo. Ujistěte se prosím, že máte otevřené a uložené řešení. To znamená, že konzola nemůže určit složku řešení. Uložení neuloženého řešení nebo vytvoření a uložení řešení, pokud ho ještě nemáte, by mělo chybu opravit.

## <a name="opening-the-console-and-console-controls"></a>Otevření konzoly a ovládacích prvků konzoly

1. Otevřete konzolu v aplikaci Visual Studio pomocí **nástrojů > správce balíčků NuGet > příkaz konzoly Správce balíčků** . Konzola je okno aplikace Visual Studio, které lze uspořádat a umístit (viz [přizpůsobení rozložení oken v aplikaci Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Ve výchozím nastavení fungují příkazy konzoly s konkrétním zdrojem a projektem balíčku jako nastavené v ovládacím prvku v horní části okna:

    ![Ovládací prvky konzoly Správce balíčků pro zdroj balíčku a projekt](media/PackageManagerConsoleControls1.png)

1. Výběr jiného zdroje balíčků nebo projektu změní tato výchozí nastavení pro následné příkazy. Pokud chcete tato nastavení overrride beze změny výchozích nastavení, je většina příkazů podporována `-Source` a `-ProjectName` Možnosti.

1. Pokud chcete spravovat zdroje balíčků, vyberte ikonu ozubeného kolečka. Jedná se o zástupce **nástrojů > možností > správce balíčků NuGet > dialogové okno zdroje balíčků** , jak je popsáno na stránce [uživatelského rozhraní Správce balíčků](install-use-packages-visual-studio.md#package-sources) . Ovládací prvek napravo od výběru projektu také vymaže obsah konzoly:

    ![Nastavení konzoly Správce balíčků a zrušení ovládacích prvků](media/PackageManagerConsoleControls2.png)

1. Tlačítko vpravo přerušuje dlouho běžící příkaz. Například při spuštění se `Get-Package -ListAvailable -PageSize 500` zobrazí seznam prvních 500 balíčků na výchozím zdroji (například NuGet.org), což může trvat několik minut.

    ![Řízení ukončení konzoly Správce balíčků](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a>Instalace balíčku

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Viz [Install-Package](../reference/ps-reference/ps-ref-install-package.md).

Instalace balíčku v konzole nástroje provádí stejný postup, jak je popsáno v tématu [co se stane, když se nainstaluje balíček](../concepts/package-installation-process.md), a to s následujícími přídavky:

- Konzola zobrazuje příslušné licenční podmínky v okně s předpokládanou smlouvou. Pokud s podmínkami nesouhlasíte, měli byste balíček hned odinstalovat.
- Také odkaz na balíček je přidán do souboru projektu a zobrazí se v **Průzkumník řešení** pod uzlem **odkazy** , je nutné projekt uložit, aby se změny v souboru projektu zobrazily přímo.

## <a name="uninstall-a-package"></a>Odinstalace balíčku

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Viz [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md). Pokud potřebujete najít identifikátor, použijte [Get-Package](../reference/ps-reference/ps-ref-get-package.md) pro zobrazení všech balíčků aktuálně nainstalovaných ve výchozím projektu.

Odinstalace balíčku provede následující akce:

- Odstraní odkazy na balíček z projektu (a jakýkoli formát správy se používá). Odkazy se již nezobrazují v **Průzkumník řešení**. (Projekt bude pravděpodobně nutné znovu sestavit, aby se zobrazila jeho odebraný ze složky **bin** .)
- Vrátí všechny změny provedené `app.config` `web.config` v nebo při instalaci balíčku.
- Odebere dříve nainstalované závislosti, pokud žádné zbývající balíčky nepoužívají tyto závislosti.

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

## <a name="find-a-package"></a>Nalezení balíčku

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

Viz [Najít-Package](../reference/ps-reference/ps-ref-find-package.md). V Visual Studio 2013 a starších verzích použijte [příkaz Get-Package](../reference/ps-reference/ps-ref-get-package.md) .

## <a name="availability-of-the-console"></a>Dostupnost konzoly

Od sady Visual Studio 2017 se NuGet a správce balíčků NuGet automaticky nainstalují, když vyberete libovolnou možnost. Úlohy s ČISTÝM vztahem; můžete ji také nainstalovat jednotlivě tím, že v instalačním programu sady Visual Studio zkontrolujete **jednotlivé součásti > nástroj Code tools > správce balíčků NuGet** .

Pokud ve Visual Studiu 2015 a starších verzích chybí správce balíčků NuGet, podívejte se na **nástroje > rozšíření a aktualizace...** a vyhledejte rozšíření Správce balíčků NuGet. Pokud nemůžete použít instalační program rozšíření v aplikaci Visual Studio, můžete si rozšíření stáhnout přímo z [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) .

Konzola správce balíčků není v Visual Studio pro Mac v současnosti k dispozici. Ekvivalentní příkazy jsou však k dispozici prostřednictvím rozhraní příkazového [řádku NuGet](../reference/nuget-exe-CLI-reference.md). Visual Studio pro Mac má uživatelské rozhraní pro správu balíčků NuGet. Viz [zahrnutí balíčku NuGet do projektu](/visualstudio/mac/nuget-walkthrough).

Konzola správce balíčků není součástí Visual Studio Code.

## <a name="extend-the-package-manager-console"></a>Rozšiřování konzoly Správce balíčků

Některé balíčky instalují nové příkazy pro konzolu nástroje. Například `MvcScaffolding` vytvoří příkazy `Scaffold` , jako jsou zobrazené níže, které generují řadiče a zobrazení ASP.NET MVC:

![Instalace a použití MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a>Nastavení profilu PowerShellu NuGet

Profil PowerShellu umožňuje, aby byly běžně používané příkazy dostupné bez ohledu na to, kde používáte PowerShell. NuGet podporuje profil specifický pro NuGet, který se obvykle nachází v následujícím umístění:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Profil najdete tak, že do `$profile` konzoly zadáte:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Další podrobnosti najdete v tématu [profily Windows PowerShellu](/previous-versions//bb613488(v=vs.85)).

## <a name="use-the-nugetexe-cli-in-the-console"></a>Použití rozhraní příkazového řádku nuget.exe v konzole nástroje

Chcete-li zpřístupnit rozhraní příkazového [ `nuget.exe` řádku](../reference/nuget-exe-cli-reference.md) v konzole správce balíčků, nainstalujte balíček [NuGet. CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) z konzoly:

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
