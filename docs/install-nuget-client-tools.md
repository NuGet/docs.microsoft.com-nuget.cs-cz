---
title: Instalace klientských nástrojů Nugetu
description: Pokyny k instalaci klientských nástrojů dotnet tak pro nuget rozhraní příkazového řádku (CLI) a Správce balíčků pro Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 6e3011493b7b89bc43cd9a267aea7fd32d668cec
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426562"
---
# <a name="install-nuget-client-tools"></a>Instalace klientských nástrojů NuGetu

> **Pokud chcete balíček nainstalovat? Zobrazit [způsoby instalace balíčků NuGet](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

Pro práci s NuGet, jako příjemce balíčku nebo autora, můžete použít nástroje rozhraní příkazového řádku (CLI) a také funkcí NuGet v sadě Visual Studio. Tento článek stručně popisuje funkce různých nástrojů, jak nainstalovat a jejich srovnávacích [dostupnost funkcí](#feature-availability). Využívání balíčků pomocí NuGet, najdete v článku [instalace a použití balíčku (rozhraní příkazového řádku .NET)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) a [instalace a použití balíčku (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). Chcete-li začít vytvářet balíčky NuGet, přečtěte si téma [vytvoření a publikování balíčku .NET Standard (rozhraní příkazového řádku dotnet)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) a [vytvoření a publikování balíčku .NET Standard (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Nástroj&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Popis | Stáhnout&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Nástroje rozhraní příkazového řádku pro knihovny .NET Core a .NET Standard a všechny sady SDK – vizuální styl projektu, například ten, který cílí na .NET Framework (viz [SDK atribut](/dotnet/core/tools/csproj#additions)). Součástí sady SDK .NET Core a poskytuje základní funkce NuGet na všech platformách. | [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Nástroj příkazového řádku pro knihovny rozhraní .NET Framework a sady SDK styl projekty, které cílit na knihovny .NET Standard. Nabízí všechny funkce NuGet na Windows, poskytuje většinu funkcí na Mac a Linux, pokud je spuštěno mono. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | Na Windows poskytuje možnosti NuGet prostřednictvím uživatelského rozhraní Správce balíčků a konzole Správce balíčků; součástí. NET související úlohy. Na počítači Mac poskytuje některé funkce přes uživatelské rozhraní. Ve Visual Studio Code jsou k dispozici NuGet funkce prostřednictvím rozšíření. | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

[Rozhraní příkazového řádku MSBuild](reference/msbuild-targets.md) také poskytuje možnost obnovení a vytváření balíčků, což je užitečné hlavně na serverech sestavení. Nástroj MSBuild není univerzální nástroj pro práci s NuGet.

## <a name="cli-tools"></a>Nástroje rozhraní příkazového řádku

Jsou dva nástroje rozhraní příkazového řádku NuGet `dotnet.exe` a `nuget.exe`. Zobrazit [dostupnost funkcí](#feature-availability) porovnání.

* Pokud chcete cílit na .NET Core nebo .NET Standard, použijte rozhraní příkazového řádku dotnet. Rozhraní příkazového řádku dotnet, je třeba formát projektu SDK – vizuální styl, který používá [SDK atribut](/dotnet/core/tools/csproj#additions).
* K cíli pomocí rozhraní .NET Framework (sada SDK styl pouze aplikace project), `nuget.exe CLI`. Pokud je projekt migrovali na `packages.config`, použijte rozhraní příkazového řádku dotnet.

### <a name="dotnetexe-cli"></a>dotnet.exe CLI

Příkazového řádku .NET Core 2.0 `dotnet.exe`, funguje na všech platformách (Windows, Mac a Linux) a poskytuje základní funkce NuGet jako je například instalace, obnovení a publikování balíčků. `dotnet` poskytuje přímou integraci se soubory projektu .NET Core (například `.csproj`), což je užitečné ve většině scénářů. `dotnet` sestavován přímo pro každou platformu a nevyžaduje instalaci součásti Mono.

Instalace:

- Na vývojových prostředích, nainstalujte [.NET Core SDK](https://aka.ms/dotnetcoregs).
- Sestavovací servery, postupujte podle pokynů [pomocí .NET Core SDK a nástroje kontinuální integrace](/dotnet/core/tools/using-ci-with-cli).

Další informace o použití základních příkazů pomocí rozhraní příkazového řádku dotnet, najdete v článku [nainstalovat a používat balíčky pomocí rozhraní příkazového řádku dotnet](consume-packages/install-use-packages-dotnet-cli.md).

### <a name="nugetexe-cli"></a>nuget.exe CLI

`nuget.exe` Rozhraní příkazového řádku, `nuget.exe`, je nástroj příkazového řádku pro Windows, který poskytuje všechny možnosti NuGet, můžete spustit také na Mac OSX a Linux pomocí [Mono](http://www.mono-project.com/docs/getting-started/install/) s určitými omezeními.

Instalace:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Použití `nuget update -self` na existující nuget.exe aktualizovat na nejnovější verzi Windows.

Další informace o použití základních příkazů s `nuget.exe` rozhraní příkazového řádku, naleznete v tématu [nainstalovat a používat balíčky pomocí rozhraní příkazového řádku nuget.exe](consume-packages/install-use-packages-nuget-cli.md).

> [!Note]
> Doporučeno na nejnovější verzi rozhraní příkazového řádku NuGet je vždy k dispozici na `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. Pro účely kompatibility se staršími systémy průběžné integrace, adresu URL předchozího `https://nuget.org/nuget.exe` v současné době poskytuje [zastaralé 2.8.6 přílohy nástroj rozhraní příkazového řádku](https://github.com/NuGet/NuGetGallery/issues/5381).

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: NuGet možnosti jsou k dispozici prostřednictvím rozšíření na webu marketplace nebo použijte `dotnet.exe` nebo `nuget.exe` nástroje rozhraní příkazového řádku.

- Visual Studio pro Mac: některé funkce NuGet jsou integrované přímo v. Zobrazit [balíček včetně NuGet ve vašem projektu](/visualstudio/mac/nuget-walkthrough) návod. Pro další možnosti, použijte `dotnet.exe` nebo `nuget.exe` nástroje rozhraní příkazového řádku.

- Visual Studio ve Windows: **Správce balíčků NuGet** je součástí sady Visual Studio 2012 a novější. Visual Studio poskytuje [uživatelské rozhraní Správce balíčků](tools/package-manager-ui.md) a [Konzola správce balíčků](tools/package-manager-console.md), pomocí které můžete spouštět většinu operací NuGet.
  - Spouští se v sadě Visual Studio 2017, instalační program obsahuje Správce balíčků NuGet u jakékoli úlohy, která využívá rozhraní .NET. Nainstalovat samostatně, nebo ověřte, zda je nainstalován Správce balíčků, spusťte instalační program sady Visual Studio a zaškrtněte možnost v rámci **jednotlivé komponenty > kód nástroje > Správce balíčků NuGet**.
  - Uživatelské rozhraní Správce balíčků a konzole jsou jedinečné pro Visual Studio na Windows. Nejsou v současné době k dispozici v sadě Visual Studio pro Mac.
  - Nástroj příkazového řádku se vyžaduje pro podporu funkcí NuGet v integrovaném vývojovém prostředí. Můžete použít buď `dotnet` rozhraní příkazového řádku nebo `nuget.exe` rozhraní příkazového řádku. `dotnet` Se některé úlohy sady Visual Studio, jako je .NET Core je nainstalované rozhraní příkazového řádku. `nuget.exe` Rozhraní příkazového řádku musí být nainstalován samostatně, jak je popsáno výše.
  - Konzola správce balíčků příkazy fungují pouze v rámci sady Visual Studio na Windows a v rámci jiných prostředí PowerShell, nebudou fungovat.
  - Pro sadu Visual Studio 2010 a starší nainstalujte "NuGet Package Manager pro rozšíření sady Visual Studio".
  - Rozšíření NuGet pro Visual Studio 2013 a 2015 si můžete také stáhnout z [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
  - Pokud chcete zobrazit náhled chystaných funkcí NuGet, nainstalujte [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), který funguje na straně po boku s stabilní verze sady Visual Studio. Pokud chcete zprávy o problémech nebo sdílet nápady verzí Preview pro služby, otevřete problém na [úložiště NuGet GitHub](https://github.com/Nuget/Home/issues).

## <a name="feature-availability"></a>Dostupnost funkcí

| Funkce | dotnet CLI | nuget rozhraní příkazového řádku (Windows) | nuget CLI (Mono) | Visual Studio (Windows) | Visual Studio for Mac |
| --- | --- | --- | --- | --- | --- |
| Hledat balíčky |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Instalace/Odinstalace balíčků | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| Aktualizace balíčků | &#10004; | &#10004; | | &#10004; | &#10004; |
| Obnovení balíčků | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| Správa informační kanály balíčků (zdroje) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Správa balíčků na informační kanál | &#10004; | &#10004; | &#10004; | | |
| Sadu klíčů rozhraní API pro informační kanály | | &#10004; | &#10004; | | |
| Vytvoření packages(3) | &#10004; | &#10004; | &#10004;(4) | &#10004; | |
| Publikovat balíčky | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Replikovat balíčky |  | &#10004; | &#10004; | | |
| Správa *globální balíčku* a složek do mezipaměti | &#10004; | &#10004; | &#10004; | | |
| Správa konfigurace NuGet | | &#10004; | &#10004; | | |

(1) nemá vliv na soubory projektu. použít `dotnet.exe` místo.

(2) pracuje jenom s `packages.config` souboru, nikoli zpětným řešení (`.sln`) soubory.

(3) různé funkce Rozšířené balíček jsou k dispozici prostřednictvím rozhraní příkazového řádku jen nejsou reprezentovány v nástrojích Visual Studio UI.

(4) funguje s `.nuspec` soubory, ale ne s soubory projektu.

### <a name="related-topics"></a>Související témata

- [Instalace a Správa balíčků s využitím sady Visual Studio](tools/package-manager-ui.md)
- [Instalace a Správa balíčků s využitím Powershellu](tools/package-manager-console.md)
- [Instalace a Správa balíčků s využitím rozhraní příkazového řádku dotnet](consume-packages/install-use-packages-dotnet-cli.md)
- [Instalace a Správa balíčků s využitím rozhraní příkazového řádku nuget.exe](consume-packages/install-use-packages-nuget-cli.md)
- [Referenční informace prostředí PowerShell konzoly Správce balíčků](tools/powershell-reference.md)
- [Vytvoření balíčku](create-packages/creating-a-package.md)
- [Publikování balíčku](nuget-org/publish-a-package.md)

Vývojáři pracující na Windows můžete také prozkoumat [NuGet – Průzkumník balíčků](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), je open source, samostatný nástroj vizuálně zkoumat, vytvořte a upravte balíčky NuGet. Je velmi užitečné, například experimentální ke změnám struktury balíčku bez nutnosti opětovného sestavení balíčku.
