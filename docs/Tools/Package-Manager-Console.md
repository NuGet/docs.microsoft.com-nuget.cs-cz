---
title: "Průvodce konzoly Správce balíčků NuGet | Microsoft Docs"
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2b92b119-6861-406c-82af-9d739af230e4
description: "Pokyny k používání konzoly Správce balíčků NuGet v sadě Visual Studio pro práci s balíčky."
keywords: "Konzole Správce balíčků NuGet, NuGet powershell, spravovat balíčky NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d9df514c6f92a3ea0841503d86c44271e70f95f2
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="package-manager-console"></a>Konzola správce balíčků

Konzola správce balíčků NuGet je integrovaná v sadě Visual Studio v systému Windows verze 2012 a novější. (Není součástí sady Visual Studio pro Mac nebo Visual Studio Code.)

Konzole vám umožní používat [příkazy prostředí NuGet PowerShell](../tools/powershell-reference.md) najít, instalaci, odinstalaci a aktualizovat balíčky NuGet. Pomocí konzoly je nutné v případech, kde uživatelského rozhraní Správce balíčků neposkytuje způsob, jak provést operaci.

Například hledání a instalaci balíčku provádí pomocí tří jednoduché kroky:

1. Otevřete projekt nebo řešení v sadě Visual Studio a otevřete pomocí konzoly **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkaz.

1. Najděte balíčku, který chcete nainstalovat. Pokud už víte, to, přeskočte ke kroku 3.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Spusťte příkaz instalace:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

V tomto tématu:

- [Otevření konzole](#opening-the-console-and-console-controls)
- [Instalace balíčku](#installing-a-package)
- [Odinstalace balíčku](#uninstalling-a-package)
- [Hledání balíčku](#finding-a-package)
- [Aktualizace balíčku](#updating-a-package)
- [Dostupnost konzoly nástroje](#availability-of-the-console)
- [Rozšíření konzole Správce balíčků](#extending-the-package-manager-console)
- [Nastavení profilu NuGet PowerShell](#setting-up-a-nuget-powershell-profile)

> [!Important]
> Všechny operace, které jsou k dispozici v konzole můžete také provést s [NuGet CLI](../tools/nuget-exe-cli-reference.md). Příkazy konzoly ale provoz v rámci kontextu Visual Studio a uložené projekt nebo řešení a často dosáhnout více než jejich ekvivalentní příkazy rozhraní příkazového řádku. Například instalaci balíčku přes konzolu přidá odkaz na projekt zatímco rozhraní příkazového řádku příkaz neexistuje. Z tohoto důvodu vývojáře, kteří pracují v sadě Visual Studio obvykle dáváte přednost, pomocí konzoly nástroje rozhraní příkazového řádku.

> [!Tip]
> Mnoho konzole operací závisí na s řešením otevřít v sadě Visual Studio s názvem známé cestě. Pokud máte neuložené řešení nebo žádné řešení, zobrazí se chyba, "řešení není otevřené nebo není uložené. Ujistěte se, že máte řešení otevřené a uložené." To znamená, že konzole nemůže určit složku řešení. Ukládání neuložené řešení, nebo vytvoření a uložení řešení, pokud nemáte otevřete, by měl opravte chybu.

## <a name="opening-the-console-and-console-controls"></a>Otevření konzoly a ovládací prvky konzoly

1. Otevřete konzolu v sadě Visual Studio pomocí **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkaz. Konzole je okno sady Visual Studio, které mohou být uspořádány a umístěný, ale chcete (viz [přizpůsobení rozložení oken v sadě Visual Studio](https://docs.microsoft.com/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Ve výchozím nastavení fungují příkazy konzoly pro určitý balíček zdrojem a projekt jako sada v ovládacím prvku v horní části okna:

    ![Ovládací prvky konzoly Správce balíčků pro zdroj balíčku a projectu](media/PackageManagerConsoleControls1.png)

1. Vyberte jiný balíček zdroje nebo projektu změní tyto výchozí hodnoty pro následné příkazy. Způsobem lze potlačit tato nastavení beze změny výchozí hodnoty, většina příkazů podporují `-Source` a `-ProjectName` možnosti.

1. Chcete-li spravovat zdroje balíčků, vyberte ikonu zařízení. Toto je zástupce **nástroje > Možnosti > Správce balíčků NuGet > zdroje balíčků** dialogové okno jak je popsáno na [uživatelského rozhraní Správce balíčků](Package-Manager-UI.md#package-sources) stránky. Ovládací prvek napravo od modulu pro výběr projektu vymaže obsah v konzole:

    ![Nastavení konzoly Správce balíčků a zrušte ovládací prvky](media/PackageManagerConsoleControls2.png)

1. Úplně vpravo tlačítko přerušení dlouho běžící příkaz. Například běžet `Get-Package -ListAvailable -PageSize 500` obsahuje seznam balíčků horní 500 na výchozí zdroj (například nuget.org), který může trvat několik minut.

    ![Konzola správce balíčků zastavení řízení](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Instalace balíčku

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

V tématu [Install-Package](../tools/ps-ref-install-package.md).

Instalaci balíčku, provede následující akce:

- Zobrazí v okně konzoly se smlouvou předpokládané příslušných licenčních podmínek. Pokud nesouhlasíte s podmínkami, byste měli okamžitě odinstalovat balíček.
- Přidá odkaz na projekt v jakémkoli formát reference je používán. Odkazy se následně zobrazí v Průzkumníku řešení a formátu souboru použít referenční. Upozorňujeme však, že s PackageReference, je nutné uložit projektu a podívejte se změny v souboru projektu přímo.
- Ukládá do mezipaměti balíčku:
    - PackageReference: balíčku je uloží do mezipaměti na `%USERPROFILE%\.nuget\packages` a zámek souboru tj `project.assets.json` se aktualizuje.
    - `packages.config`: vytvoří `packages` složky v kořenové řešení a zkopíruje soubory balíčku do podsložky v něm. `package.config` Aktualizaci souboru.
- Aktualizace `app.config` nebo `web.config` Pokud balíček používá [zdroje a konfiguračním souboru transformace](../create-packages/source-and-config-file-transformations.md).
- Nainstaluje všechny závislosti, pokud ještě není přítomný v projektu. To může aktualizovat verze balíčku v procesu, jak je popsáno v [řešení závislostí](../consume-packages/dependency-resolution.md).
- Zobrazí soubor readme balíčku, pokud je k dispozici, v okně Visual Studio.

> [!Tip]
> Jednou z výhod primární instalace balíčků s `Install-Package` příkaz v konzole je, který přidá odkaz na projekt stejně, jako by se použít uživatelské rozhraní Správce balíčků. Naopak `nuget install` rozhraní příkazového řádku příkaz pouze stáhne balíček a automaticky nepřidá odkaz.

## <a name="uninstalling-a-package"></a>Odinstalace balíčku

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

V tématu [odinstalovat balíček](../tools/ps-ref-uninstall-package.md). Použití [Get-Package](../tools/ps-ref-get-package.md) zobrazíte všechny balíčky, které jsou aktuálně nainstalované ve výchozím projektu, pokud potřebujete najít identifikátor.

Odinstalace balíčku, provede následující akce:

- Odebere odkazy na balíček z projektu (a jakýkoli formát odkaz se používá). Odkazy se nebude zobrazovat v Průzkumníku řešení. (Možná budete muset znovu sestavte projekt nevidíte odebrán z **Bin** složky.)
- Vrátí zpět změny provedené v `app.config` nebo `web.config` Pokud byl balíček nainstalován.
- Pokud žádné zbývající balíčky pomocí těchto závislostí odebere dříve nainstalovali závislosti.

> [!Tip]
> Jako `Install-Package`, `Uninstall-Package` příkaz má výhodu Správa odkazů v projektu, na rozdíl od `nuget uninstall` rozhraní příkazového řádku příkaz.

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

V tématu [Get-Package](../tools/ps-ref-get-package.md) a [balíčku aktualizace](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>Hledání balíčku

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

V tématu [najít balíček](../tools/ps-ref-find-package.md). V sadě Visual Studio 2013 a starší, použijte [Get-Package](../tools/ps-ref-get-package.md) místo.

## <a name="availability-of-the-console"></a>Dostupnost konzoly nástroje

V aplikaci Visual Studio 2017 NuGet a Správce balíčků NuGet jsou automaticky nainstalovány po výběru některé. Úlohy související s NET; Můžete také nainstalovat ji jednotlivě kontrolou **jednotlivých součástí > Code nástroje > Správce balíčků NuGet** možnosti v instalačním programu Visual Studio 2017.

Zkontrolujte také, pokud jste chybí Správce balíčků NuGet v sadě Visual Studio 2015 a starší, **nástroje > rozšíření a aktualizace...**  a vyhledejte rozšíření Správce balíčků NuGet. Pokud nemůžete použít instalační program rozšíření v sadě Visual Studio, si můžete stáhnout rozšíření přímo z [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

Konzola správce balíčků není v současné době dostupné pomocí sady Visual Studio for Mac. Ekvivalentní příkazy, ale jsou k dispozici prostřednictvím [NuGet CLI](nuget-exe-CLI-reference.md). Visual Studio pro Mac nemá uživatelského rozhraní pro správu balíčků NuGet. V tématu [balíček včetně NuGet ve vašem projektu](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).

Konzola správce balíčků není součástí Visual Studio Code.

## <a name="extending-the-package-manager-console"></a>Rozšíření konzole Správce balíčků

Některé balíčky nainstalujte nové příkazy pro konzolu. Například `MvcScaffolding` vytvoří příkazy, jako je `Scaffold` vidíte níže, který generuje kontrolery a zobrazení ASP.NET MVC:

![Instalace a použití MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Nastavení profilu NuGet prostředí PowerShell

Profil prostředí PowerShell umožňuje zpřístupnit běžně používané příkazy bez ohledu na pomocí prostředí PowerShell. NuGet podporuje NuGet konkrétní profil většinou nacházejí v následujícím umístění:

```
%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Chcete-li vyhledat profil, zadejte `$profile` v konzole:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Další podrobnosti najdete v části [profily Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).
