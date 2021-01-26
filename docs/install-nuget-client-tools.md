---
title: Instalace nástrojů klienta NuGet
description: Pokyny k instalaci klientských nástrojů, rozhraní příkazového řádku dotnet a NuGet (CLI) a správce balíčků pro Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 0e3938fc1ac748285ba26541a7d4e907c9a64156
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775900"
---
# <a name="install-nuget-client-tools"></a>Instalace klientských nástrojů NuGetu

> **Chcete nainstalovat balíček? Viz [způsoby instalace balíčků NuGet](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

Pro práci s NuGet, jako příjemce balíčku nebo autor, můžete použít nástroje rozhraní příkazového řádku (CLI) a také funkce NuGet v aplikaci Visual Studio. Tento článek stručně popisuje možnosti různých nástrojů, způsob jejich instalace a jejich srovnávací [dostupnost funkcí](#feature-availability). Pokud chcete začít používat balíčky NuGet ke využívání balíčků, přečtěte si téma [instalace a použití balíčku (DOTNET CLI)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) a [instalace a použití balíčku (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). Chcete-li začít vytvářet balíčky NuGet, přečtěte si téma [Vytvoření a publikování balíčku .NET Standard (DOTNET CLI)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) a [Vytvoření a publikování balíčku .NET Standard (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Štětec&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Popis | Stáhnout&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Nástroj rozhraní příkazového řádku pro knihovny .NET Core a .NET Standard a pro libovolný [projekt ve stylu sady SDK](resources/check-project-format.md) , jako je například jeden, který cílí .NET Framework. Je součástí .NET Core SDK a poskytuje základní funkce NuGet na všech platformách. (Počínaje sadou Visual Studio 2017 se rozhraní příkazového řádku dotnet automaticky instaluje se všemi úlohami souvisejícími s .NET Core.)| [Sada .NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Nástroj rozhraní příkazového řádku pro knihovny .NET Framework a pro všechny projekty, které [nejsou ve stylu sady SDK](resources/check-project-format.md) , jako je například jeden, který cílí na .NET Standard knihovny. Poskytuje všechny funkce NuGet ve Windows a poskytuje většinu funkcí v systémech Mac a Linux, když běží v mono. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | V systému Windows je **Správce balíčků NuGet** součástí sady Visual Studio 2012 a novějších. Sada Visual Studio poskytuje [uživatelské rozhraní Správce balíčků](consume-packages/install-use-packages-visual-studio.md) a [konzolu Správce balíčků](consume-packages/install-use-packages-powershell.md), pomocí kterých můžete spouštět většinu operací NuGet. | [Visual Studio](https://www.visualstudio.com/downloads/) |
| [Visual Studio pro Mac](/visualstudio/mac/nuget-walkthrough) | V systému Mac jsou některé funkce NuGet integrované přímo. Konzola správce balíčků není aktuálně k dispozici. Další možnosti získáte pomocí nástrojů rozhraní příkazového `dotnet.exe` `nuget.exe` řádku nebo.  | [Visual Studio pro Mac](https://visualstudio.microsoft.com/vs/mac/) |
| [Visual Studio Code](https://code.visualstudio.com/docs) | V systémech Windows, Mac nebo Linux jsou možnosti NuGet dostupné prostřednictvím rozšíření Marketplace nebo pomocí nástrojů rozhraní příkazového `dotnet.exe` `nuget.exe` řádku (CLI). | [Visual Studio Code](https://code.visualstudio.com/Download/)|

Rozhraní příkazového [řádku MSBuild](reference/msbuild-targets.md) také poskytuje možnost obnovení a vytváření balíčků, které jsou primárně užitečné na serverech sestavení. Nástroj MSBuild není obecným nástrojem pro práci s NuGet.

Příkazy konzoly Správce balíčků fungují jenom v sadě Visual Studio ve Windows a nefungují v jiných prostředích PowerShellu.

## <a name="visual-studio"></a>Visual Studio
### <a name="install-on-visual-studio-2017-and-newer"></a>Nainstalovat do sady Visual Studio 2017 a novější
Od verze Visual Studio 2017 instalační program zahrnuje Správce balíčků NuGet se všemi úlohami, které využívají .NET. Chcete-li nainstalovat nástroj samostatně nebo ověřit, zda je nainstalován Správce balíčků, spusťte instalační program sady Visual Studio a zaškrtněte možnost v části **jednotlivé komponenty > nástroje kódu > správce balíčků NuGet**.

### <a name="install-on-visual-studio-2015-and-older"></a>Nainstalovat do sady Visual Studio 2015 a starší
Rozšíření NuGet pro Visual Studio 2013 a 2015 je možné stáhnout z [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) .

V případě sady Visual Studio 2010 a starší verze nainstalujte "rozšíření Správce balíčků NuGet pro Visual Studio". Všimněte si, že pokud se rozšíření na první stránce výsledků hledání nezobrazuje, zkuste změnit rozevírací seznam řazení podle na "nejvíc stahování" nebo abecední řazení.

## <a name="cli-tools"></a>Nástroje rozhraní příkazového řádku
`dotnet` `nuget.exe` K podpoře funkcí NuGet v integrovaném vývojovém prostředí (IDE) můžete použít rozhraní příkazového řádku nebo rozhraní příkazového řádku. Rozhraní `dotnet` příkazového řádku se instaluje s některými úlohami sady Visual Studio, jako je například .NET Core. Rozhraní příkazového `nuget.exe` řádku se musí nainstalovat samostatně, jak je popsáno výše.

Existují dva nástroje rozhraní příkazového řádku NuGet `dotnet.exe` a `nuget.exe` . Porovnání najdete v tématu [dostupnost funkcí](#feature-availability) .

* Chcete-li cílit na rozhraní .NET Core nebo .NET Standard, použijte rozhraní příkazového řádku dotnet. Rozhraní příkazového `dotnet` řádku je vyžadováno pro formát projektu ve stylu sady SDK, který používá [atribut SDK](/dotnet/core/tools/csproj#additions).
* Chcete-li cílit na .NET Framework (pouze projekt ve stylu sady SDK), použijte rozhraní příkazového `nuget.exe` řádku. Pokud je projekt migrován z aplikace `packages.config` do PackageReference, použijte rozhraní příkazového řádku dotnet.

### <a name="dotnetexe-cli"></a>dotnet.exe CLI

Rozhraní příkazového řádku .NET Core 2,0, které `dotnet.exe` funguje na všech platformách (Windows, Mac a Linux) a poskytuje základní funkce NuGet, jako je instalace, obnovení a publikování balíčků. `dotnet` poskytuje přímou integraci se soubory projektu .NET Core (například `.csproj` ), které jsou ve většině scénářů užitečné. `dotnet` je také sestaven přímo pro každou platformu a nevyžaduje instalaci mono.

Instalace:

- V vývojářských počítačích nainstalujte [.NET Core SDK](https://aka.ms/dotnetcoregs). Počínaje sadou Visual Studio 2017 se rozhraní příkazového řádku dotnet automaticky nainstaluje se všemi úlohami souvisejícími s .NET Core.
- Pro sestavovací servery postupujte podle pokynů v tématu [použití .NET Core SDK a nástrojů v nepřetržité integraci](/dotnet/core/tools/using-ci-with-cli).

Pokud chcete zjistit, jak používat základní příkazy s rozhraním příkazového řádku dotnet, přečtěte si téma [instalace a použití balíčků pomocí rozhraní příkazového řádku dotnet](consume-packages/install-use-packages-dotnet-cli.md).

### <a name="nugetexe-cli"></a>nuget.exe CLI

`nuget.exe`CLI `nuget.exe` je nástroj příkazového řádku pro Windows, který poskytuje všechny možnosti NuGet. dá se taky spustit na počítačích Mac OSX a Linux pomocí [mono](https://www.mono-project.com/docs/getting-started/install/) s některými omezeními.

Informace o tom, jak používat základní příkazy s rozhraním `nuget.exe` příkazového řádku, najdete v tématu [instalace a použití balíčků pomocí nuget.exe CLI](consume-packages/install-use-packages-nuget-cli.md).

Instalace:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Pomocí `nuget update -self` systému Windows můžete aktualizovat existující nuget.exe na nejnovější verzi.

> [!Note]
> Nejnovější Doporučené rozhraní NuGet CLI je vždy k dispozici na adrese `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe` . Pro účely kompatibility se staršími systémy kontinuální integrace (předchozí adresa URL) `https://nuget.org/nuget.exe` aktuálně poskytuje [zastaralý nástroj CLI 2.8.6](https://github.com/NuGet/NuGetGallery/issues/5381).

## <a name="feature-availability"></a>Dostupnost funkcí

| Funkce | dotnet CLI | rozhraní příkazového řádku NuGet (Windows) | rozhraní příkazového řádku NuGet (mono) | Visual Studio (Windows) | Visual Studio pro Mac |
| --- | --- | --- | --- | --- | --- |
| Vyhledat balíčky |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Instalace/odinstalace balíčků | &#10004; | &#10004; (1) | &#10004; | &#10004; | &#10004; |
| Balíčky aktualizací | &#10004; | &#10004; | | &#10004; | &#10004; |
| Obnovení balíčků | &#10004; | &#10004; | &#10004; (2) | &#10004; | &#10004; |
| Správa informačních kanálů balíčků (zdrojů) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Správa balíčků v informačním kanálu | &#10004; | &#10004; | &#10004; | | |
| Nastavení klíčů rozhraní API pro informační kanály | | &#10004; | &#10004; | | |
| Vytváření balíčků (3) | &#10004; | &#10004; | &#10004; (4) | &#10004; | |
| Publikování balíčků | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Replikace balíčků |  | &#10004; | &#10004; | | |
| Spravovat *globální balíčky* a složky mezipaměti | &#10004; | &#10004; | &#10004; | | |
| Spravovat konfiguraci NuGet | | &#10004; | &#10004; | | |

(1) nemá vliv na soubory projektu; `dotnet.exe` místo toho použijte.

(2) funguje pouze se `packages.config` soubory řešení ( `.sln` ).

(3) v rozhraní příkazového řádku jsou k dispozici různé pokročilé funkce balíčku, protože nejsou reprezentované v nástrojích uživatelského rozhraní sady Visual Studio.

(4) pracuje se `.nuspec` soubory, ale ne se soubory projektu.

## <a name="upcoming-features"></a>Nadcházející funkce
Pokud chcete zobrazit náhled nadcházejících funkcí NuGet, nainstalujte [Visual Studio Preview](https://www.visualstudio.com/vs/preview/), které funguje souběžně se stabilními verzemi sady Visual Studio. K nahlášení problémů nebo sdílení nápadů pro verze Preview otevřete problém v [úložišti GitHub NuGet](https://github.com/Nuget/Home/issues).

### <a name="related-topics"></a>Související témata

- [Instalace a Správa balíčků pomocí sady Visual Studio](consume-packages/install-use-packages-visual-studio.md)
- [Instalace a Správa balíčků pomocí PowerShellu](consume-packages/install-use-packages-powershell.md)
- [Instalace a Správa balíčků pomocí příkazu dotnet CLI](consume-packages/install-use-packages-dotnet-cli.md)
- [Instalace a Správa balíčků pomocí nuget.exe CLI](consume-packages/install-use-packages-nuget-cli.md)
- [Reference k prostředí PowerShell konzoly Správce balíčků](reference/powershell-reference.md)
- [Vytvoření balíčku](create-packages/creating-a-package.md)
- [Publikování balíčku](nuget-org/publish-a-package.md)

Vývojáři, kteří pracují na Windows, mohou také prozkoumat [Průzkumníka balíčků NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), open source a samostatný nástroj pro vizuální zkoumání, vytváření a úpravy balíčků NuGet. Je velmi užitečné, například pokud chcete provádět experimentální změny ve struktuře balíčku bez nového sestavení balíčku.
