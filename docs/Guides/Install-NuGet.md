---
title: "Instalace nástrojů klienta NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "Pokyny k instalaci klienta nástroje, rozhraní příkazového řádku (CLI) a Správce balíčků pro sadu Visual Studio."
keywords: "nuget.exe rozhraní příkazového řádku, nástrojích klienta NuGet, Správce balíčků NuGet, konzoly Správce balíčků NuGet, NuGet pro Visual Studio, NuGet beta kanálu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2f67c298d269149bba9f36ad9e026d5443c39b6a
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="installing-nuget-client-tools"></a>Instalace nástrojů klienta NuGet

> [!Tip]
> **Hledáte nainstalovat balíček? V tématu [rychlý start - použití balíček](../Quickstart/Use-a-Package.md).**

Existují dvě primární nástroje, které vám pomůžou vytvářet, publikovat a využívat balíčky NuGet:

1. [ **NuGet CLI** ](#nuget-cli) je nástroj příkazového řádku pro Windows, který nabízí všechny funkce NuGet; může být spuštěn také na Mac OSX a Linux pomocí Mono nebo prostřednictvím rozhraní příkazového řádku .NET Core (`dotnet`).
1. [ **Správce balíčků NuGet v sadě Visual Studio** ](#nuget-package-manager-in-visual-studio) (jenom Windows) je nástroj grafického uživatelského rozhraní pro správu balíčků a zahrnuje konzole prostředí PowerShell, pomocí kterého můžete určité příkazy pro balíčky NuGet přímo v rámci Visual Studio. Uživatelské rozhraní Správce balíčků a konzoly jsou obě zahrnutá v sadě Visual Studio (v systému Windows) 2012 a novější a může být nainstalován ručně pro starší verze.

    Pomocí sady Visual Studio pro Mac NuGet možnosti jsou součástí přímo. V tématu [balíček včetně NuGet ve vašem projektu](/visualstudio/mac/nuget-walkthrough) návod.

    Visual Studio Code v současnosti nemá žádné integrovanou podporu NuGet. Pomocí rozhraní příkazového řádku NuGet nebo [dotnet rozhraní příkazového řádku](../Tools/dotnet-Commands.md).

Rozhraní příkazového řádku NuGet a Správce balíčků podporují následující operace:

- Hledání balíčků
- Instalovat balíčky
- Balíčky aktualizací
- Odinstalaci balíčků
- Obnovení balíčků (uživatelského rozhraní pouze v Správce balíčků)
- Spravovat zdroje NuGet

Následující funkce jsou podporovány pouze v rozhraní příkazového řádku NuGet:

- Správa balíčků (nuget.org nebo privátní informační kanál)
- Vytvoření balíčků 
- Publikování balíčků
- Spravovat soubor nuget.config.
- Správě ukládání do mezipaměti NuGet
- Replikace balíčku

> [!Note]
> Dobrý dalším nástrojem je [Explorer balíček NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), nástroj na open source, samostatné vizuálně zkoumat, vytvořit a upravit balíčky NuGet. Je třeba velmi užitečné, změnit experimentální struktura balíček bez nutnosti znovu sestavte balíček pokaždé, když.
> Napříč platformami [.NET Core rozhraní příkazového řádku](/dotnet/articles/core/tools/index#installation) nástrojů, použít pro vývoj aplikací .NET Core podporuje několik příkazy pro balíčky NuGet, například odstranit, místní hodnoty, push, aktualizací Service pack a obnovení. 

## <a name="nuget-cli"></a>Rozhraní příkazového řádku NuGet

Rozhraní příkazového řádku NuGet poskytuje přístup k všechny možnosti NuGet a lze spustit ve Windows, Mac OSX a Linux, jak je popsáno v následujících částech.

### <a name="windows"></a>Windows

**Přímé stahování:**

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> U balíčku NuGet 1.4 +, můžete použít `nuget update -self` aktualizovat vaše stávající nuget.exe na nejnovější verzi.

**Ostatní metody:**

- **Chocolatey**: Nainstalujte [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey balíčku pomocí [Chocolatey](http://chocolatey.org) klienta. 

    ```ps
    choco install nuget.commandline
    ```

- **Visual Studio**: Nainstalujte [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) balíček z konzoly Správce balíčků v sadě Visual Studio.

    > [!Note]
    > **Pro uživatele 2.x NuGet**: z důvodu nejnovější změny zavedené v NuGet 3.2 [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) body na nejnovější stabilní verze 2.x NuGet aby průběžnou integraci systémů z potenciálně ukončování řádků.

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a>Mac OSX a Linux

Na Mac OSX a Linux existují dva způsoby, jak spustit rozhraní NuGet příkazového řádku:

- Nainstalujte [.NET Core SDK](https://www.microsoft.com/net/download/core), což zahrnuje základních možností NuGet. Soubory ke stažení jsou také uvedeny na [github.com/dotnet/cli](https://github.com/dotnet/cli). Pokud potřebujete úplnější možnosti, použijte druhý níže uvedenou možnost používat `nuget.exe` s Mono.

- Nainstalujte [Mono](http://www.mono-project.com/docs/getting-started/install/) a potom pomocí `nuget.exe` spustitelného souboru příkazového řádku pro Windows (verze 3.2 a novější) z [nuget.org/downloads](https://nuget.org/downloads). Systémem NuGet Mono podléhá následující omezení:

    - Postup testování příkazy:
        - Konfigurace
        - Odstranit
        - Nápověda
        - Instalace
        - list
        - Push
        - setApiKey
        - Zdroje
        - specifikace

    - Částečně pracovní příkazy:
        - Sada: funguje s `.nuspec` soubory, ale ne soubory projektu.
        - obnovení: funguje s `packages.config` a `project.json` soubory, ale ne při řešení (`.sln`) soubory.

    - Příkazy, které nefungují:
        - Aktualizace

### <a name="related-topics"></a>Související témata

- [Referenční dokumentace rozhraní příkazového řádku NuGet](../tools/nuget-exe-cli-reference.md)
- [Vytváření balíčku](../create-packages/creating-a-package.md)
- [Publikování balíčku](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a>Správce balíčků NuGet v sadě Visual Studio

Správce balíčků NuGet je zahrnuta v každé edici sady Visual Studio v systému Windows 2012 a novější. Obsahuje uživatelského rozhraní Správce balíčků ([odkaz](../tools/package-manager-ui.md)) a konzola Správce balíčků, pomocí kterého se dostanete nástroje, které jsou součástí určitých balíčků ([odkaz](../tools/package-manager-console.md)).

Instalační program Visual Studio 2017 zahrnuje Správce balíčků NuGet s libovolnou úlohu, kterou využívá rozhraní .NET. Chcete-li instalovat samostatně, nebo ověřte, zda je nainstalován Správce balíčků, spusťte instalační program Visual Studio 2017 a zkontrolujte příslušné možnosti v nabídce **jednotlivých součástí > Code nástroje > Správce balíčků NuGet**.

> [!Note]
> Konzole vyžaduje [prostředí PowerShell 2.0](http://support.microsoft.com/kb/968929), která již bude nainstalován ve Windows 7 nebo novější a Windows Server 2008 R2 nebo vyšší.
>
> Konzola správce balíčků příkazy také fungovat pouze v sadě Visual Studio v systému Windows. Pomocí rozhraní příkazového řádku NuGet mimo prostředí, včetně pomocí sady Visual Studio pro Mac a Visual Studio Code.

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a>Instalace Správce balíčků pro Visual Studio 2010 a starší

*Tyto kroky nejsou potřebné pro sadu Visual Studio 2012 a novějším, které již obsahují Správce balíčků.*

1. V sadě Visual Studio 2010 a starší, klikněte na tlačítko **nástroje > rozšíření a aktualizace**.
1. Přejděte na **Online**, vyhledejte "NuGet balíček správce pro Visual Studio" a klikněte na **Stáhnout**.
1. V dialogovém okně instalačního programu klikněte na **nainstalovat**.
1. Po dokončení instalace restartujte Visual Studio.

> [!Tip]
> Pokud nelze použít **rozšíření a aktualizace** dialogové okno v sadě Visual Studio (například jeho blokován bránou proxy serveru), si můžete stáhnout rozšíření pro Visual Studio 2013 a 2015 přímo na [https://dist.nuget.org/ index.HTML](https://dist.nuget.org/index.html).

### <a name="updating-the-package-manager"></a>Aktualizace Správce balíčků

Pro Visual Studio 2015 Update 2 nebo novější správce balíčku se automaticky aktualizují na nejnovější stabilní verze.

Pro Visual Studio 2015 Update 1 a starší, vyberte **nástroje > rozšíření a aktualizace** příkaz a klikněte na **aktualizace** a zda je k dispozici nová verze Správce balíčků.  

### <a name="nuget-previews"></a>Verze Preview NuGet

Pokud chcete zobrazit náhled chystaných funkcí NuGet, nainstalujte [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), který funguje souběžného s stabilní verze sady Visual Studio.

Všimněte si, že předchozí Beta NuGet kanálu (`https://dotnet.myget.org/F/nuget-beta/vsix/`) pro Visual Studio 2015 se už používá.

Chcete odesílat zprávy o problémech s libovolnou verzi aplikace NuGet nebo sdílet nápady, otevřete na problém [úložiště NuGet GitHub](https://github.com/Nuget/Home).

### <a name="related-topics"></a>Související témata

- [Odkaz uživatelského rozhraní Správce balíčků](../tools/package-manager-ui.md)
- [Konzola správce balíčků odkaz](../tools/package-manager-console.md)
- [Referenční informace prostředí PowerShell konzoly Správce balíčků](../tools/powershell-reference.md)