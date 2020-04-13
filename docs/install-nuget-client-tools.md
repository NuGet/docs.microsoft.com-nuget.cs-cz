---
title: Instalace klientských nástrojů NuGet
description: Pokyny k instalaci klientských nástrojů, rozhraní příkazového řádku dotnet a nuget (CLI) a Správce balíčků pro sady Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 2769f0ef0373b26eedb4bac6242fee0e814310c5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428819"
---
# <a name="install-nuget-client-tools"></a>Instalace klientských nástrojů NuGetu

> **Hledáte instalaci balíčku? Viz [Způsoby instalace balíčků NuGet](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

Chcete-li pracovat s NuGet, jako příjemce balíčku nebo tvůrce, můžete použít nástroje rozhraní příkazového řádku (CLI) stejně jako NuGet funkce v sadě Visual Studio. Tento článek stručně popisuje možnosti různých nástrojů, jak je nainstalovat a jejich [dostupnost srovnávacích funkcí](#feature-availability). Chcete-li začít používat NuGet využívat balíčky, najdete v [tématu Instalace a použití balíčku (dotnet CLI)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) a [nainstalovat a použít balíček (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). Chcete-li začít vytvářet balíčky NuGet, přečtěte si informace [o vytvoření a publikování balíčku NET Standard (dotnet CLI)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) a vytvoření a publikování balíčku NET Standard [(Visual Studio).](quickstart/create-and-publish-a-package-using-visual-studio.md)

| Nástroj&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Popis | Ke stažení&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Nástroj rozhraní CLI pro knihovny .NET Core a .NET Standard a pro jakýkoli [projekt ve stylu sady SDK,](resources/check-project-format.md) například projekt, který cílí na rozhraní .NET Framework. Součástí sady .NET Core SDK a poskytuje základní funkce NuGet na všech platformách. (Počínaje Visual Studio 2017, dotnet CLI se automaticky nainstaluje s libovolnými úlohami souvisejícími s jádrem .NET.)| [Sada .NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Nástroj rozhraní CLI pro knihovny rozhraní .NET Framework a pro jakýkoli projekt, který [není ve stylu sady SDK,](resources/check-project-format.md) například ten, který cílí na knihovny .NET Standard. Poskytuje všechny funkce NuGet v systému Windows, poskytuje většinu funkcí na Mac a Linux při spuštění v rámci Mono. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | V systému Windows **je Správce balíčků NuGet** součástí sady Visual Studio 2012 a novější. Visual Studio poskytuje [ui Správce balíčků](consume-packages/install-use-packages-visual-studio.md) a [konzolu správce balíčků](consume-packages/install-use-packages-powershell.md), pomocí kterých můžete spustit většinu operací NuGet. | [Visual Studio](https://www.visualstudio.com/downloads/) |
| [Visual Studio pro Mac](/visualstudio/mac/nuget-walkthrough) | Na Macu jsou některé funkce NuGet integrované přímo. Konzola Správce balíčků není v současné době k dispozici. Pro další funkce `dotnet.exe` použijte `nuget.exe` nástroje nebo CLI.  | [Visual Studio pro Mac](https://visualstudio.microsoft.com/vs/mac/) |
| [Visual Studio Code](https://code.visualstudio.com/docs) | Ve Windows, Macu nebo Linuxu jsou funkce NuGet dostupné `dotnet.exe` `nuget.exe` prostřednictvím rozšíření marketplace nebo pomocí nástrojů nebo CLI. | [Visual Studio Code](https://code.visualstudio.com/Download/)|

[MSBuild CLI](reference/msbuild-targets.md) také poskytuje možnost obnovit a vytvořit balíčky, což je užitečné především na serverech sestavení. MSBuild není univerzální nástroj pro práci s NuGet.

Příkazy konzoly Správce balíčků fungují pouze v sadě Visual Studio v systému Windows a nefungují v jiných prostředích prostředí PowerShell.

## <a name="visual-studio"></a>Visual Studio
### <a name="install-on-visual-studio-2017-and-newer"></a>Instalace v Sadě Visual Studio 2017 a novější
Počínaje Visual Studio 2017, instalátor zahrnuje NuGet Správce balíčků s jakékoli úlohy, které zaměstnává .NET. Chcete-li nainstalovat samostatně nebo ověřit, zda je nainstalován Správce balíčků, spusťte instalační program sady Visual Studio a zaškrtněte možnost v části **Jednotlivé součásti > kód > správce balíčků NuGet**.

### <a name="install-on-visual-studio-2015-and-older"></a>Instalace v Sadě Visual Studio 2015 a starší
Rozšíření NuGet pro Visual Studio 2013 a 2015 lze stáhnout z [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

Pro Visual Studio 2010 a starší, nainstalujte rozšíření "NuGet Package Manager pro Visual Studio". Všimněte si, že pokud rozšíření na první stránce výsledků hledání nevidíte, zkuste změnit rozevírací seznam Seřadit podle na "Nejvíce stažených souborů" nebo abecední řazení.

## <a name="cli-tools"></a>Nástroje cli
Můžete použít `dotnet` buď CLI `nuget.exe` nebo CLI pro podporu NuGet funkce v ide. Rozhraní `dotnet` se konzistou CLI je nainstalováno s některými úlohami sady Visual Studio, jako je například .NET Core. ClI `nuget.exe` musí být nainstalována samostatně, jak je popsáno výše.

Dva nástroje ClI NuGet jsou `dotnet.exe` a `nuget.exe`. Zobrazení [dostupnosti funkcí](#feature-availability) pro porovnání.

* Chcete-li cílit na rozhraní .NET Core nebo .NET Standard, použijte rozhraní SE kontinuu pro dotnet. Příkaz `dotnet` příkaz příkazpříkaz je vyžadován pro formát projektu ve stylu sady SDK, který používá [atribut SDK](/dotnet/core/tools/csproj#additions).
* Chcete-li cílit na rozhraní .NET Framework (pouze `nuget.exe` projekt bez sdk), použijte rozhraní se klis. Pokud je projekt migrován z `packages.config` PackageReference, použijte dotnet CLI.

### <a name="dotnetexe-cli"></a>Rozhraní se kontitu dotnet.exe

Rozhraní .NET Core 2.0 `dotnet.exe`CLI , funguje na všech platformách (Windows, Mac a Linux) a poskytuje základní funkce NuGet, jako je instalace, obnovení a publikování balíčků. `dotnet`poskytuje přímou integraci se soubory projektu `.csproj`.NET Core (například ), což je užitečné ve většině scénářů. `dotnet`je také postaven přímo pro každou platformu a nevyžaduje instalaci Mono.

Instalace:

- Do vývojářských počítačů nainstalujte sadu [.NET Core SDK](https://aka.ms/dotnetcoregs). Počínaje Visual Studio 2017, dotnet CLI se automaticky nainstaluje s všechny úlohy související s jádrem .NET.
- Servery sestavení postupujte podle pokynů [k použití sady .NET Core SDK a nástrojů v průběžné integraci](/dotnet/core/tools/using-ci-with-cli).

Informace o použití základních příkazů pomocí rozhraní příkazu dotnet CLI naleznete v [tématu Instalace a použití balíčků pomocí rozhraní příkazového příkazu dotnet .](consume-packages/install-use-packages-dotnet-cli.md)

### <a name="nugetexe-cli"></a>Rozhraní příkazového řádku nuget.exe

`nuget.exe` Příkaz cli, `nuget.exe`, je nástroj příkazového řádku pro systém Windows, který poskytuje všechny funkce NuGet; to může být také spuštěnna Mac OSX a Linux pomocí [Mono](https://www.mono-project.com/docs/getting-started/install/) s některými omezeními.

Informace o použití základních příkazů `nuget.exe` pomocí příkazového příkazu naleznete v [tématu Instalace a použití balíčků pomocí příkazového příkazu nuget.exe](consume-packages/install-use-packages-nuget-cli.md).

Instalace:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> V `nuget update -self` systému Windows slouží k aktualizaci existujícího programu nuget.exe na nejnovější verzi.

> [!Note]
> Nejnovější doporučené rozhraní příkazového příkazu `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`NuGet je vždy k dispozici na adrese . Pro účely kompatibility se staršími systémy `https://nuget.org/nuget.exe` průběžné integrace poskytuje předchozí adresa URL v současné době [již zastaralou sadu 2.8.6 CLI .](https://github.com/NuGet/NuGetGallery/issues/5381)

## <a name="feature-availability"></a>Dostupnost funkcí

| Funkce | Rozhraní příkazového řádku dotnet | nuget CLI (Windows) | nuget CLI (Mono) | Visual Studio (Windows) | Visual Studio for Mac |
| --- | --- | --- | --- | --- | --- |
| Hledat balíčky |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Instalace/odinstalace balíčků | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| Aktualizovat balíčky | &#10004; | &#10004; | | &#10004; | &#10004; |
| Obnovení balíčků | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| Správa zdrojů balíčků (zdroje) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Správa balíčků ve zdroji | &#10004; | &#10004; | &#10004; | | |
| Nastavení klíčů rozhraní API pro informační kanály | | &#10004; | &#10004; | | |
| Vytvořit balíčky(3) | &#10004; | &#10004; | &#10004;(4) | &#10004; | |
| Publikování balíčků | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Replikovat balíčky |  | &#10004; | &#10004; | | |
| Správa *složek globálních balíčků* a mezipaměti | &#10004; | &#10004; | &#10004; | | |
| Spravovat konfiguraci NuGet | | &#10004; | &#10004; | | |

(1) Nemá vliv na soubory projektu; místo `dotnet.exe` toho použít.

(2) Pracuje `packages.config` pouze se souborem`.sln`a ne s řešením ( ) soubory.

(3) Různé funkce rozšířené balíček jsou k dispozici prostřednictvím rozhraní příkazového příkazu pouze jako nejsou zastoupeny v nástrojích visual studio ui.

(4) Pracuje `.nuspec` se soubory, ale ne se soubory projektu.

## <a name="upcoming-features"></a>Nadcházející funkce
Pokud chcete zobrazit náhled nadcházejících funkcí NuGet, nainstalujte [visual studio preview](https://www.visualstudio.com/vs/preview/), který funguje vedle sebe se stabilními verzemi sady Visual Studio. Chcete-li nahlásit problémy nebo sdílet nápady pro náhledy, otevřete problém v [úložišti NuGet GitHub](https://github.com/Nuget/Home/issues).

### <a name="related-topics"></a>Související témata

- [Instalace a správa balíčků pomocí sady Visual Studio](consume-packages/install-use-packages-visual-studio.md)
- [Instalace a správa balíčků pomocí PowerShellu](consume-packages/install-use-packages-powershell.md)
- [Instalace a správa balíčků pomocí rozhraní SE kontinua DOTNET](consume-packages/install-use-packages-dotnet-cli.md)
- [Instalace a správa balíčků pomocí cli nuget.exe](consume-packages/install-use-packages-nuget-cli.md)
- [Odkaz na konzolu Správce balíčků powershellu](reference/powershell-reference.md)
- [Vytvoření balíčku](create-packages/creating-a-package.md)
- [Publikování balíčku](nuget-org/publish-a-package.md)

Vývojáři pracující v systému Windows můžete také prozkoumat [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), open source, samostatný nástroj vizuálně prozkoumat, vytvořit a upravit balíčky NuGet. Je velmi užitečné například provést experimentální změny ve struktuře balíčku bez opětovného sestavení balíčku.
