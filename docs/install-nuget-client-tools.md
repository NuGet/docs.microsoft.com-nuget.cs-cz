---
title: Instalace nástrojů klienta NuGet
description: Pokyny k instalaci klienta nástrojů dotnet a nuget rozhraní příkazového řádku (CLI) a Správce balíčků pro sadu Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 04/09/2018
ms.topic: quickstart
ms.openlocfilehash: f136295cd46dd11a153b5f9c25a685a5a8dbd45a
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818118"
---
# <a name="installing-nuget-client-tools"></a>Instalace nástrojů klienta NuGet

> **Hledáte nainstalovat balíček? V tématu [způsoby instalace balíčků NuGet](consume-packages/ways-to-install-a-package.md).**

Chcete-li pracovat s NuGet, jako balíček příjemce nebo creator, můžete použít [nástrojů rozhraní příkazového řádku (CLI)](#cli-tools) a také [funkce NuGet v sadě Visual Studio](#visual-studio). Tento článek stručně popisuje možnosti různých nástrojů, jak nainstalovat a jejich srovnávacích [dostupnost funkcí](#feature-availability). Chcete-li začít používat využívat balíčky NuGet, přečtěte si téma [instalací a použitím balíčku (.NET rozhraní příkazového řádku)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) a [instalací a použitím balíčku (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). Chcete-li začít vytvářet balíčky NuGet, přečtěte si téma [vytvořit a publikovat balíček NET Standard (dotnet rozhraní příkazového řádku)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) a [vytvoření a publikování balíčku NET Standard (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Nástroj&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Popis | Stahování&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Součástí rozhraní .NET Core SDK a poskytuje základní funkce NuGet na všech platformách. | [.NET core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Nabízí všechny funkce NuGet v systému Windows, při spuštění v Mono obsahuje většinu funkcí na Mac a Linux. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | V systému Windows poskytuje možnosti NuGet prostřednictvím uživatelského rozhraní Správce balíčků a konzoly Správce balíčků; součástí. NET související úlohy. V systému Mac poskytuje určité funkce prostřednictvím uživatelského rozhraní. V sadě Visual Studio Code NuGet funkce poskytované prostřednictvím rozšíření. | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

[Rozhraní příkazového řádku nástroje MSBuild](reference/msbuild-targets.md) také nabízí možnost obnovení a vytváření balíčků, což je užitečné hlavně na serverech sestavení. MSBuild není nástroj pro obecné účely pro práci s NuGet.

## <a name="cli-tools"></a>Nástrojů příkazového řádku

Jsou dva NuGet rozhraní příkazového řádku nástroje `dotnet.exe` a `nuget.exe`. V tématu [dostupnost funkcí](#feature-availability) pro porovnání.

### <a name="dotnetexe-cli"></a>dotnet.exe CLI

Rozhraní .NET Core 2.0 příkazového řádku, `dotnet.exe`, funguje na všech platformách (Windows, Mac a Linux) a poskytuje základní funkce NuGet jako je instalace, obnovení a publikování balíčků. `dotnet` poskytuje přímá integrace s .NET Core soubory projektu (například `.csproj`), což je užitečné, ve většině scénářů. `dotnet` je také vytvořené přímo pro každou platformu a nevyžaduje instalaci Mono.

Instalace:

- Na počítačích vývojářů, nainstalujte [.NET Core SDK](https://aka.ms/dotnetcoregs).
- U serverů, sestavení, postupujte podle pokynů [pomocí rozhraní .NET Core SDK a nástrojů v průběžnou integraci](/dotnet/core/tools/using-ci-with-cli).

Další informace najdete v tématu [.NET Core rozhraní příkazového řádku nástroje](/dotnet/core/tools/index?tabs=netcore2x#tabpanel_fXL5YCOYDa_netcore2x).

### <a name="nugetexe-cli"></a>nuget.exe rozhraní příkazového řádku

Rozhraní příkazového řádku NuGet `nuget.exe`, je nástroj příkazového řádku pro Windows, který nabízí všechny funkce NuGet; můžete spustit také na Mac OSX a Linux pomocí [Mono](http://www.mono-project.com/docs/getting-started/install/) s omezeními. Na rozdíl od `dotnet`, `nuget.exe` rozhraní příkazového řádku nemá vliv na soubory projektu a neaktualizuje `packages.config` při instalaci balíčků.

Instalace:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Použití `nuget update -self` v systému Windows k aktualizaci existující nuget.exe na nejnovější verzi.

> [!Note]
> Nejnovější doporučená rozhraní příkazového řádku NuGet je vždy k dispozici na `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. Pro účely kompatibility se staršími systémy průběžnou integraci a adresu URL předchozí `https://nuget.org/nuget.exe` aktuálně poskytuje [zastaralé 2.8.6 přílohy rozhraní příkazového řádku nástroje](https://github.com/NuGet/NuGetGallery/issues/5381).

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: NuGet možnosti jsou k dispozici prostřednictvím rozšíření marketplace, nebo použít `dotnet.exe` nebo `nuget.exe` nástrojů příkazového řádku.

- Visual Studio pro Mac: některé funkce NuGet jsou vytvořené přímo. V tématu [balíček včetně NuGet ve vašem projektu](/visualstudio/mac/nuget-walkthrough) návod. Pro další možnosti, použijte `dotnet.exe` nebo `nuget.exe` nástrojů příkazového řádku.

- Visual Studio v systému Windows: **Správce balíčků NuGet** je součástí sady Visual Studio 2012 a novějším. Poskytuje správce balíčků [uživatelského rozhraní Správce balíčků](tools/package-manager-ui.md) a [Konzola správce balíčků](tools/package-manager-console.md), pomocí kterého můžete spustit většinu operací NuGet.
  - Instalační program Visual Studio 2017 zahrnuje Správce balíčků NuGet s libovolnou úlohu, kterou využívá rozhraní .NET. Chcete-li instalovat samostatně, nebo ověřte, zda je nainstalován Správce balíčků, spusťte instalační program Visual Studio 2017 a zkontrolujte příslušné možnosti v nabídce **jednotlivých součástí > Code nástroje > Správce balíčků NuGet**.
  - Uživatelské rozhraní Správce balíčků a konzoly jsou jedinečné pro Visual Studio v systému Windows. Nejsou k dispozici v současné době v sadě Visual Studio for Mac.
  - Visual Studio automaticky nezahrnuje `nuget.exe` rozhraní příkazového řádku, které je nutné nainstalovat samostatně, jak je popsáno výše.
  - Konzola správce balíčků příkazy fungovat pouze v sadě Visual Studio v systému Windows a nefungují v jiných prostředích prostředí PowerShell.
  - Pro sadu Visual Studio 2010 a starší nainstalujte rozšíření "NuGet balíček správce pro Visual Studio".
  - Rozšíření NuGet pro Visual Studio 2013 a 2015 můžete také stáhnout z [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
  - Pokud chcete zobrazit náhled chystaných funkcí NuGet, nainstalujte [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), který funguje souběžného s stabilní verze sady Visual Studio. Pokud chcete odesílat zprávy o problémech nebo sdílet nápady pro verze Preview, otevřete na problém [úložiště NuGet GitHub](https://github.com/Nuget/Home/issues).

## <a name="feature-availability"></a>Dostupnost funkcí

| Funkce | DotNet rozhraní příkazového řádku | nuget rozhraní příkazového řádku (Windows) | nuget rozhraní příkazového řádku (Mono) | Visual Studio (Windows) | Visual Studio for Mac |
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
| Spravovat *globální balíček* a složek do mezipaměti | &#10004; | &#10004; | &#10004; | | |
| Spravovat konfiguraci NuGet | | &#10004; | &#10004; | | |

(1) balíčky na pouze nuget.org

(2) nemá vliv na soubory projektu; použít `dotnet.exe` místo.

(3) funguje pouze s `packages.config` souboru a nikoli s řešení (`.sln`) soubory.

(4) různé funkce Rozšířené balíček jsou k dispozici prostřednictvím rozhraní příkazového řádku pouze, protože se nenachází v nástrojích Visual Studio uživatelského rozhraní.

(5) funguje s `.nuspec` soubory, ale ne soubory projektu.

### <a name="related-topics"></a>Související témata

- [Příkazy dotnet](tools/dotnet-commands.md)
- [Referenční dokumentace rozhraní příkazového řádku NuGet](tools/nuget-exe-cli-reference.md)
- [Odkaz uživatelského rozhraní Správce balíčků](tools/package-manager-ui.md)
- [Konzola správce balíčků odkaz](tools/package-manager-console.md)
- [Referenční informace prostředí PowerShell konzoly Správce balíčků](tools/powershell-reference.md)
- [Vytvoření balíčku](create-packages/creating-a-package.md)
- [Publikování balíčku](create-packages/publish-a-package.md)

Můžete také zkoumat vývojáře, kteří pracují v systému Windows [Explorer balíček NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), nástroj na open source, samostatné vizuálně zkoumat, vytvořit a upravit balíčky NuGet. Je například velmi užitečné, změnit experimentální struktura balíček bez nutnosti opětovného sestavení balíčku.
