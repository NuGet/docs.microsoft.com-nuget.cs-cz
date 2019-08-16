---
title: Nejčastější dotazy k NuGet
description: Běžné otázky a odpovědi pro používání NuGetu na příkazovém řádku a v aplikaci Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9b12b1fa27308cf41b58b0c244ea648d3eecdc95
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520558"
---
# <a name="nuget-frequently-asked-questions"></a>Nejčastější dotazy k NuGet

**Co je potřeba ke spuštění NuGet?**

Všechny informace o uživatelském rozhraní a nástrojích příkazového řádku jsou k dispozici v [instalační příručce](../install-nuget-client-tools.md).

**Podporuje NuGet mono?**

Nástroj příkazového řádku, `nuget.exe`, vytvoří a spustí v mono 3.2 + a může vytvářet balíčky v mono.

I `nuget.exe` když funguje plně ve Windows, jsou známé problémy v systémech Linux a OS X. Projděte si informace o [problémech mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) na GitHubu.

[Grafický klient](https://github.com/mrward/monodevelop-nuget-addin) je k dispozici jako doplněk pro MonoDevelop.

**Jak zjistím, co balíček obsahuje a jestli je pro moji aplikaci stabilní a užitečný?**

Primární zdroj pro učení o balíčku je jeho stránka se seznamem na nuget.org (nebo jiném privátním informačním kanálu). Každá stránka balíčku v nuget.org obsahuje popis balíčku, jeho historii verzí a statistiku využití. Část **informace** na stránce balíček obsahuje také odkaz na web projektu, kde obvykle najdete mnoho příkladů a další dokumentaci, která vám pomůžou zjistit, jak se balíček používá.

Další informace najdete v tématu [vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>NuGet v aplikaci Visual Studio

**Jak se podporuje NuGet v různých produktech sady Visual Studio?**

- Sada Visual Studio ve Windows podporuje [uživatelské rozhraní Správce balíčků](../consume-packages/install-use-packages-visual-studio.md) a [konzolu Správce balíčků](../consume-packages/install-use-packages-powershell.md).
- Visual Studio pro Mac obsahuje integrované funkce NuGet, jak je popsáno v tématu [zahrnutí balíčku NuGet do projektu](/visualstudio/mac/nuget-walkthrough).
- Visual Studio Code (všechny platformy) nemá žádnou přímou integraci NuGet. Použijte rozhraní příkazového [řádku NuGet](../reference/nuget-exe-cli-reference.md) nebo rozhraní příkazového [řádku dotnet](../reference/dotnet-commands.md).
- Azure DevOps poskytuje [krok sestavení pro obnovení balíčků NuGet](/vsts/build-release/tasks/package/nuget). [V Azure DevOps můžete také hostovat kanály privátního balíčku NuGet](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).

**Návody ověřit přesnou verzi nástrojů NuGet, které jsou nainstalované?**

V aplikaci Visual Studio použijte **nápovědu > o Microsoft Visual Studio** příkaz a podívejte se na verzi zobrazenou vedle **Správce balíčků NuGet**.

Případně můžete spustit konzolu Správce balíčků (**Nástroje > Správce balíčků NuGet > konzolu Správce balíčků**) a `$host` zadáním zobrazíte informace o NuGet včetně verze.

**Jaké programovací jazyky podporuje NuGet?**

NuGet je obecně funkční pro jazyky .NET a je navržena k převedení knihoven .NET do projektu. Protože podporuje také automatizaci nástroje MSBuild a sady Visual Studio v některých typech projektů, podporuje také jiné projekty a jazyky do různých stupňů.

Nejnovější verze NuGet podporuje C#, Visual Basic, F#, WIX a. C++

**Jaké šablony projektů podporuje NuGet?**

NuGet má plnou podporu pro celou řadu šablon projektů, jako jsou Windows, web, Cloud, SharePoint, WIX a tak dále.

**Návody balíčky aktualizací, které jsou součástí šablon sady Visual Studio?**

V uživatelském rozhraní Správce balíčků otevřete kartu **aktualizace** a vyberte **Aktualizovat vše** [ `Update-Package` ](../reference/ps-reference/ps-ref-update-package.md) nebo použijte příkaz z konzoly Správce balíčků.

Chcete-li aktualizovat vlastní šablonu, je nutné ručně aktualizovat úložiště šablon. Podívejte se na [blog Xavier](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) pro denákle na tomto předmětu. Všimněte si, že se jedná o vlastní riziko, protože ruční aktualizace mohou poškodit šablonu, pokud není nejnovější verze všech závislostí vzájemně kompatibilní.

**Můžu použít NuGet mimo Visual Studio?**

Ano, NuGet funguje přímo z příkazového řádku. Přečtěte si příručku k [instalaci](../install-nuget-client-tools.md) a [odkaz CLI](../reference/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>Příkazový řádek NuGet

**Návody získat nejnovější verzi nástroje příkazového řádku NuGet?**

Projděte si [příručku Instalace](../install-nuget-client-tools.md). Chcete-li zjistit aktuální nainstalovanou verzi nástroje, použijte `nuget help`.

**Jaká je licence pro NuGet. exe?**

Je možné znovu distribuovat NuGet. exe za podmínek licence MIT. Zodpovídáte za aktualizaci a obsluhu všech kopií nástroje NuGet. exe, který se rozhodnete znovu distribuovat.

**Je možné nástroj příkazového řádku NuGet zvětšit?**

Ano, do `nuget.exe`je možné přidat vlastní příkazy, jak je popsáno v [příspěvku na Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Konzola správce balíčků NuGet (Visual Studio ve Windows)

**Návody získat přístup k objektu DTE v konzole správce balíčků?**

Objekt nejvyšší úrovně v objektovém modelu automatizace sady Visual Studio se nazývá objekt DTE (vývojové nástroje prostředí). Konzola poskytuje tuto proměnnou prostřednictvím proměnné s názvem `$DTE`. Další informace najdete v tématu [Přehled modelu automatizace](/visualstudio/extensibility/internals/automation-model-overview) v dokumentaci rozšiřitelnosti sady Visual Studio.

**Snažím se přetypovat $DTE proměnnou na typ DTE2, ale zobrazí se chyba: Hodnotu "EnvDTE. DTEClass" typu "EnvDTE. DTEClass" nelze převést na typ "EnvDTE80. DTE2". Co je?**

Jedná se o známý problém s tím, jak prostředí PowerShell spolupracuje s objektem COM. Vyzkoušejte následující:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface`je pomocná funkce, kterou přidal hostitel PowerShellu NuGet.

## <a name="creating-and-publishing-packages"></a>Vytváření a publikování balíčků

**Návody seznam můj balíček v informačním kanálu?**

Viz [Vytvoření a publikování balíčku](../quickstart/create-and-publish-a-package.md).

**Mám více verzí knihovny, která cílí na různé verze .NET Framework. Návody sestavit jeden balíček, který tuto podporu podporuje?**

Viz [Podpora více .NET Framework verzí a profilů](../create-packages/supporting-multiple-target-frameworks.md).

**Návody nastavit vlastní úložiště nebo informační kanál?**

Podívejte se na téma [Přehled hostujících balíčků](../hosting-packages/overview.md).

**Jak mohu hromadně nahrávat balíčky do svého informačního kanálu NuGet?**

Viz [hromadné publikování balíčků NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Práce s balíčky

**Jaký je rozdíl mezi balíčkem na úrovni projektu a balíčkem na úrovni řešení?**

Balíček na úrovni řešení (NuGet 3. x +) je v řešení nainstalovaný jenom jednou a pak je k dispozici pro všechny projekty v řešení. Balíček na úrovni projektu je nainstalován v každém projektu, který ho používá. Balíček na úrovni řešení může také nainstalovat nové příkazy, které lze volat v konzole správce balíčků.

**Je možné balíčky NuGet nainstalovat bez připojení k Internetu?**

Ano, další informace [o tom, jak získat přístup k nugetu v případě nedostatku NuGet.org (nebo jste na rovině)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (Hanselman.com), najdete v blogovém příspěvku Scott Hanselman.

**Návody instalovat balíčky v jiném umístění než výchozí složka balíčků?**

[`repositoryPath`](../reference/nuget-config-file.md#config-section) Nastavte nastavení`Nuget.Config` pomocí .`nuget config -set repositoryPath=<path>`

**Návody se vyhnout přidání složky balíčků NuGet do správy zdrojového kódu?**

Nastavte na [`disableSourceControlIntegration`.](../reference/nuget-config-file.md#solution-section) `Nuget.Config` `true` Tento klíč funguje na úrovni řešení, a proto musí být do `$(Solutiondir)\.nuget\Nuget.Config` souboru přidán. Povolením obnovení balíčku ze sady Visual Studio se tento soubor automaticky vytvoří.

**Návody vypnout obnovení balíčků?**

Viz [povolení a zakázání obnovení balíčku](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).

**Proč se při instalaci místního balíčku se vzdálenými závislostmi zobrazí chybová zpráva "nelze vyřešit chybu závislostí?"**

Při instalaci místního balíčku do projektu je nutné vybrat možnost **všechny** zdroje. Tato část agreguje všechny informační kanály namísto použití jediného. Důvodem této chyby je, že uživatelé místního úložiště často chtějí vyhnout nechtěné instalaci vzdáleného balíčku kvůli podnikovým zásadám.

**Ve stejné složce mám více projektů, jak můžu použít samostatné soubory Packages. config pro každý projekt?**

Ve většině projektů, kde samostatné projekty jsou v samostatných složkách živé, to není problém, protože NuGet identifikuje `packages.config` soubory v jednotlivých projektech. Pomocí NuGet 3.3 + a více projektů ve stejné složce můžete vložit název projektu do `packages.config` názvů souborů pomocí vzoru `packages.{project-name}.config`a nástroj NuGet tento soubor použije.

Nejedná se o problém při použití PackageReference, protože každý soubor projektu obsahuje vlastní seznam závislostí.

**V seznamu úložišť nevidím nuget.org, jak se dá získat zpátky?**

- Přidejte `https://api.nuget.org/v3/index.json` do seznamu zdrojů nebo
- Odstraňte `%appdata%\.nuget\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) a umožněte novému vytvoření NuGet.
