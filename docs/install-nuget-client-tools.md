---
title: "Instalace nástrojů klienta NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/24/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Pokyny k instalaci klienta nástrojů dotnet a nuget rozhraní příkazového řádku (CLI) a Správce balíčků pro sadu Visual Studio."
keywords: "DotNet.exe rozhraní příkazového řádku, nuget.exe rozhraní příkazového řádku, nástrojích klienta NuGet, Správce balíčků NuGet, konzoly Správce balíčků NuGet, NuGet pro Visual Studio, NuGet beta kanálu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b94da0ea6a6b7f1e269767a7395d81c3a97a2d0c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="installing-nuget-client-tools"></a>Instalace nástrojů klienta NuGet

> **Hledáte nainstalovat balíček? V tématu [rychlý start - použití balíček](quickstart/use-a-package.md).**

Chcete-li pracovat s NuGet, jako balíček příjemce nebo creator, můžete použít [multiplatformního rozhraní příkazového řádku (CLI) nástroje](#cli-tools) a také [funkce NuGet v sadě Visual Studio](#visual-studio). Tento článek stručně popisuje možnosti různých nástrojů, jak nainstalovat a jejich srovnávacích [dostupnost funkcí](#feature-availability).

| Nástroj&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Popis | Stahování&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Součástí rozhraní .NET Core SDK a poskytuje základní funkce NuGet na všech platformách. | [.NET core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Nabízí všechny funkce NuGet v systémech Windows a většinu funkcí spuštěna pod [Mono](http://www.mono-project.com/docs/getting-started/install/) na Mac a Linux. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | Poskytuje možnosti NuGet prostřednictvím uživatelského rozhraní Správce balíčků a konzoly Správce balíčků. | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

[Rozhraní příkazového řádku nástroje MSBuild](schema/msbuild-targets.md) také nabízí možnost obnovení a vytváření balíčků, což je užitečné hlavně na serverech sestavení. MSBuild jinak není nástroj pro obecné účely pro práci s NuGet.

## <a name="cli-tools"></a>Nástrojů příkazového řádku

Jsou dva NuGet rozhraní příkazového řádku nástroje `dotnet.exe` a `nuget.exe`. V tématu [dostupnost funkcí](#feature-availability) pro porovnání.

### <a name="dotnetexe-cli"></a>dotnet.exe CLI

Rozhraní .NET Core 2.0 příkazového řádku, `dotnet.exe`, funguje na všech platformách (Windows, Mac a Linux) a poskytuje základní funkce NuGet, jako je instalace, obnovení a publikování balíčků. 'dotnet' poskytuje přímá integrace s .NET Core soubory projektu (například `.csproj`), což je užitečné, ve většině scénářů. `dotnet`je také vytvořené přímo pro každou platformu a nevyžaduje instalaci Mono.

Instalace:

- Na počítačích vývojářů, nainstalujte [.NET Core SDK](https://aka.ms/dotnetcoregs).
- U serverů, sestavení, postupujte podle pokynů [pomocí rozhraní .NET Core SDK a nástrojů v průběžnou integraci](/dotnet/core/tools/using-ci-with-cli).

Další informace najdete v tématu [.NET Core rozhraní příkazového řádku nástroje](/dotnet/core/tools/index?tabs=netcore2x#tabpanel_fXL5YCOYDa_netcore2x).

### <a name="nugetexe-cli"></a>nuget.exe CLI

Rozhraní příkazového řádku NuGet `nuget.exe`, je nástroj příkazového řádku pro Windows, který nabízí všechny funkce NuGet; můžete spustit také na Mac OSX a Linux pomocí Mono s omezeními. Na rozdíl od `dotnet`, `nuget.exe` rozhraní příkazového řádku nemá vliv na soubory projektu.

Instalace:

[!INCLUDE[install-cli](includes/install-cli.md)]

> [!Tip]
> Použití `nuget update -self` aktualizovat existující nuget.exe na nejnovější verzi.

> [!Note]
> Nejnovější doporučená rozhraní příkazového řádku NuGet je vždy k dispozici na `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. Pro účely kompatibility se staršími systémy průběžnou integraci a adresu URL předchozí `https://nuget.org/nuget.exe` vždy poskytuje 2.8.6 přílohy nástroj příkazového řádku.

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: NuGet možnosti jsou k dispozici prostřednictvím rozšíření marketplace, nebo použít `dotnet.exe` nebo `nuget.exe` nástrojů příkazového řádku.
- Visual Studio pro Mac: některé funkce NuGet jsou vytvořené přímo. V tématu [balíček včetně NuGet ve vašem projektu](/visualstudio/mac/nuget-walkthrough) návod. Pro další možnosti, použijte `dotnet.exe` nebo `nuget.exe` nástrojů příkazového řádku.

- Visual Studio v systému Windows: **Správce balíčků NuGet** je součástí sady Visual Studio 2012 a novějším. Poskytuje správce balíčků [uživatelského rozhraní Správce balíčků](tools/package-manager-ui.md) a [Konzola správce balíčků](tools/package-manager-console.md), pomocí kterého můžete spustit většinu operací NuGet.
  - Uživatelské rozhraní Správce balíčků a konzoly jsou jedinečné pro Visual Studio v systému Windows. Nejsou k dispozici v sadě Visual Studio pro Mac v současné době.
  - Visual Studio automaticky nezahrnuje `nuget.exe` rozhraní příkazového řádku, které je nutné nainstalovat samostatně, jak je popsáno výše.
  - Konzola správce balíčků příkazy lze použít pouze v sadě Visual Studio v systému Windows a ne do dalších prostředí PowerShell.
  - Instalační program Visual Studio 2017 zahrnuje Správce balíčků NuGet s libovolnou úlohu, kterou využívá rozhraní .NET. Chcete-li instalovat samostatně, nebo ověřte, zda je nainstalován Správce balíčků, spusťte instalační program Visual Studio 2017 a zkontrolujte příslušné možnosti v nabídce **jednotlivých součástí > Code nástroje > Správce balíčků NuGet**.
  - Pro sadu Visual Studio 2010 a starší nainstalujte rozšíření "NuGet balíček správce pro Visual Studio".
  - Rozšíření NuGet pro Visual Studio 2013 a 2015 můžete také stáhnout z [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
  - Pokud chcete zobrazit náhled chystaných funkcí NuGet, nainstalujte [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), který funguje souběžného s stabilní verze sady Visual Studio. Pokud chcete odesílat zprávy o problémech nebo sdílet nápady pro verze Preview, otevřete na problém [úložiště NuGet GitHub](https://github.com/Nuget/Home/issues).

## <a name="feature-availability"></a>Dostupnost funkcí

| Funkce | dotnet CLI | nuget rozhraní příkazového řádku (Windows) | nuget rozhraní příkazového řádku (Mono) | Visual Studio (Windows) | Visual Studio for Mac |
| --- | --- | --- | --- | --- | --- |
| Hledání balíčků |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Instalace nebo odinstalace balíčků | &#10004;(1) | &#10004;(2) | &#10004; | &#10004; | &#10004; |
| Balíčky aktualizací | &#10004; | &#10004; | | &#10004; | &#10004; |
| obnovení balíčků | &#10004; | &#10004; | &#10004;(3) | &#10004; | &#10004; |
| Správa informačních kanálů balíčku (zdroji) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Správa balíčků na informační kanál | &#10004;(1) | &#10004; | &#10004; | | |
| Sada rozhraní API klíče pro informační kanály | | &#10004; | &#10004; | | |
| Vytvoření packages(4) | &#10004; | &#10004; | &#10004;(5) | &#10004; | |
| Publikování balíčků | &#10004;(1) | &#10004; | &#10004; | &#10004; |  |
| Replikovat balíčky |  | &#10004; | &#10004; | | |
| Správě ukládání do mezipaměti NuGet | &#10004; | &#10004; | &#10004; | | |
| Spravovat konfiguraci NuGet | | &#10004; | &#10004; | | |

(1) balíčky na pouze nuget.org

(2) nemá vliv na soubory projektu; použít `dotnet.exe` místo.

(3) funguje pouze s `packages.config` souboru a nikoli s řešení (`.sln`) soubory.

(4) různé funkce Rozšířené balíček jsou k dispozici prostřednictvím rozhraní příkazového řádku pouze, protože se nenachází v nástrojích Visual Studio uživatelského rozhraní.

(5) funguje s `.nuspec` soubory, ale ne soubory projektu.

### <a name="related-topics"></a>Související témata

- [příkazy DotNet.](tools/dotnet-commands.md)
- [Referenční dokumentace rozhraní příkazového řádku NuGet](tools/nuget-exe-cli-reference.md)
- [Odkaz uživatelského rozhraní Správce balíčků](tools/package-manager-ui.md)
- [Konzola správce balíčků odkaz](tools/package-manager-console.md)
- [Referenční informace prostředí PowerShell konzoly Správce balíčků](tools/powershell-reference.md)
- [Vytváření balíčku](create-packages/creating-a-package.md)
- [Publikování balíčku](create-packages/publish-a-package.md)

Můžete také zkoumat vývojáře, kteří pracují v systému Windows [Explorer balíček NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), nástroj na open source, samostatné vizuálně zkoumat, vytvořit a upravit balíčky NuGet. Je například velmi užitečné, změnit experimentální struktura balíček bez nutnosti opětovného sestavení balíčku.
