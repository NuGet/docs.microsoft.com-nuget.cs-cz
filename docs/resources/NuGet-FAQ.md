---
title: NuGet často kladené otázky
description: Běžné otázky a odpovědi pro použití NuGet na příkazovém řádku a v sadě Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 8cc990e0c9eed07c59c8dffb04d104be47051736
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "69999942"
---
# <a name="nuget-frequently-asked-questions"></a>NuGet nejčastější dotazy

Nejčastější dotazy týkající se NuGet.org, například NuGet.org otázky k účtu, naleznete [v NuGet.org často kladených otázkách](../nuget-org/nuget-org-faq.md).

**Co je nutné ke spuštění NuGet?**

Všechny informace o nástroji ui i příkazového řádku jsou k dispozici v [průvodci instalací](../install-nuget-client-tools.md).

**Podporuje NuGet Mono?**

Nástroj příkazového řádku `nuget.exe`, , sestaví a spustí pod Mono 3.2+ a můžete vytvořit balíčky v Mono.

Ačkoli `nuget.exe` funguje plně na Windows, existují známé problémy na Linuxu a OS X. Viz [Problémy Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) na GitHubu.

[Grafický klient](https://github.com/mrward/monodevelop-nuget-addin) je k dispozici jako doplněk pro MonoDevelop.

**Jak zjistím, co balíček obsahuje a zda je stabilní a užitečný pro mou aplikaci?**

Primárním zdrojem pro učení o balíčku je jeho výpis stránky na nuget.org (nebo jiný soukromý zdroj). Každá stránka balíčku na nuget.org obsahuje popis balíčku, jeho historii verzí a statistiky využití. Část **Informace** na stránce balíčku také obsahuje odkaz na web projektu, kde obvykle najdete mnoho příkladů a další dokumentaci, která vám pomůže zjistit, jak se balíček používá.

Další informace naleznete v [tématu Hledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>NuGet v sadě Visual Studio

**Jak je NuGet podporován v různých produktech sady Visual Studio?**

- Visual Studio v systému Windows podporuje [ui Správce balíčků](../consume-packages/install-use-packages-visual-studio.md) a [konzolu Správce balíčků](../consume-packages/install-use-packages-powershell.md).
- Visual Studio pro Mac má integrované funkce NuGet, jak je popsáno na [včetně balíčku NuGet v projektu](/visualstudio/mac/nuget-walkthrough).
- Visual Studio Code (všechny platformy) nemá žádné přímé NuGet integrace. Použijte [rozhraní se konstituce NuGet](../reference/nuget-exe-cli-reference.md) nebo [rozhraní se kontinu pro dotnet](../reference/dotnet-commands.md).
- Azure DevOps poskytuje [krok sestavení k obnovení balíčků NuGet](/vsts/build-release/tasks/package/nuget). Můžete také [hostovat privátní nugetové kanály balíčků v Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).

**Jak lze zkontrolovat přesnou verzi nástrojů NuGet, které jsou nainstalovány?**

V sadě Visual Studio použijte příkaz **Nápověda > o aplikaci Microsoft Visual Studio** a podívejte se na verzi zobrazenou vedle **správce balíčků NuGet**.

Případně spusťte konzolu Správce balíčků **(Nástroje > NuGet Správce balíčků > konzoli správce balíčků)** a zadejte `$host` informace o NuGet včetně verze.

**Jaké programovací jazyky jsou podporovány NuGet?**

NuGet obecně funguje pro jazyky .NET a je navržen tak, aby knihovny .NET do projektu. Vzhledem k tomu, že také podporuje automatizaci MSBuild a Visual Studio v některých typech projektů, podporuje také jiné projekty a jazyky v různých stupních.

Nejnovější verze NuGet podporuje C#, Visual Basic, F#, WiX a C++.

**Jaké šablony projektů jsou podporovány nugetem?**

NuGet má plnou podporu pro různé šablony projektů, jako jsou Windows, Web, Cloud, SharePoint, Wix a tak dále.

**Jak lze aktualizovat balíčky, které jsou součástí šablon sady Visual Studio?**

Přejděte na kartu **Aktualizace** v uzdu Správce balíčků a vyberte **Aktualizovat vše**nebo použijte [ `Update-Package` příkaz](../reference/ps-reference/ps-ref-update-package.md) z konzoly Správce balíčků.

Chcete-li aktualizovat samotnou šablonu, musíte ručně aktualizovat úložiště šablon. Viz [Xavier Decoster blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) na toto téma. Všimněte si, že se to provádí na vlastní nebezpečí, protože ruční aktualizace může poškodit šablonu, pokud nejnovější verze všech závislostí nejsou vzájemně kompatibilní.

**Je možné použít NuGet mimo Visual Studio?**

Ano, NuGet funguje přímo z příkazového řádku. Viz [průvodce instalací](../install-nuget-client-tools.md) a [odkaz na vzpona v nařízení o vyřizování mu sekacího systému](../reference/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>Příkazový řádek NuGet

**Jak získám nejnovější verzi nástroje příkazového řádku NuGet?**

Viz [průvodce instalací](../install-nuget-client-tools.md). Chcete-li zkontrolovat aktuální nainstalovanou `nuget help`verzi nástroje, použijte .

**Jaká je licence pro nuget.exe?**

Můžete distribuovat nuget.exe podle podmínek licence MIT. Jste zodpovědní za aktualizaci a údržbu všech kopií nuget.exe, které se rozhodnete redistribuovat.

**Je možné rozšířit nástroj příkazového řádku NuGet?**

Ano, je možné přidat vlastní příkazy , `nuget.exe`jak je popsáno v [příspěvku Roba Reynolda](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Konzola Správce balíčků NuGet (Visual Studio v systému Windows)

**Jak získám přístup k objektu DTE v konzole Správce balíčků?**

Objekt nejvyšší úrovně v objektovém modelu automatizace sady Visual Studio se nazývá objekt DTE (Development Tools Environment). Konzola poskytuje prostřednictvím `$DTE`proměnné s názvem . Další informace naleznete v [tématu Přehled modelu automatizace](/visualstudio/extensibility/internals/automation-model-overview) v dokumentaci k rozšiřitelnosti sady Visual Studio.

**Snažím se přetypovat proměnnou $DTE na typ DTE2, ale zobrazí se chyba: Nelze převést hodnotu "EnvDTE.DTEClass" typu "EnvDTE.DTEClass" na typ "EnvDTE80.DTE2". Co je?**

Toto je známý problém s tím, jak prostředí PowerShell spolupracuje s objektem COM. Vyzkoušejte následující kroky:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface`je pomocná funkce přidaná hostitelem prostředí NuGet PowerShell.

## <a name="creating-and-publishing-packages"></a>Vytváření a publikování balíčků

**Jak mohu uvést svůj balíček v informačním kanálu?**

Viz [Vytvoření a publikování balíčku](../quickstart/create-and-publish-a-package.md).

**Mám více verzí knihovny, které cílí na různé verze rozhraní .NET Framework. Jak vytvořím jeden balíček, který to podporuje?**

Viz [Podpora více verzí a profilů rozhraní .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).

**Jak si nastavím vlastní úložiště nebo informační kanál?**

Podívejte se na [přehled hostingových balíčků](../hosting-packages/overview.md).

**Jak mohu nahrát balíčky do mého NuGet feed hromadně?**

Viz [Hromadné publikování balíčků NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Práce s balíčky

**Jaký je rozdíl mezi balíčkem na úrovni projektu a balíčkem na úrovni řešení?**

Balíček na úrovni řešení (NuGet 3.x+) je nainstalován pouze jednou v řešení a je pak k dispozici pro všechny projekty v řešení. Balíček na úrovni projektu je nainstalován v každém projektu, který jej používá. Balíček na úrovni řešení může také nainstalovat nové příkazy, které lze volat z konzoly Správce balíčků.

**Je možné nainstalovat balíčky NuGet bez připojení k Internetu?**

Ano, viz příspěvek blogu Scotta Hanselmana [Jak získat přístup k NuGetu, když je nuget.org vypnutý (nebo jste v letadle)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).

**Jak nainstaluji balíčky do jiného umístění než výchozí složka balíčků?**

Nastavte [`repositoryPath`](../reference/nuget-config-file.md#config-section) nastavení `Nuget.Config` v `nuget config -set repositoryPath=<path>`použití .

**Jak se vyhnout přidání složky balíčky NuGet do správy zdrojového kódu?**

Nastavte [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` `true`na . Tento klíč funguje na úrovni řešení, a `$(Solutiondir)\.nuget\Nuget.Config` proto je třeba přidat do souboru. Povolení obnovení balíčku z aplikace Visual Studio vytvoří tento soubor automaticky.

**Jak vypnu obnovení balíčku?**

Viz [Povolení a zakázání obnovení balíčku](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).

**Proč se při instalaci místního balíčku se vzdálenými závislostmi zobrazuje chyba "Nelze vyřešit chybu závislostí"?**

Při instalaci místního balíčku do projektu je třeba vybrat zdroj **Vše.** Tím se agreguje všechny kanály namísto použití pouze jednoho. Důvodem, proč se tato chyba zobrazuje, je to, že uživatelé místního úložiště se často chtějí vyhnout náhodné instalaci vzdáleného balíčku kvůli firemním vazbám.

**Mám více projektů ve stejné složce, jak mohu použít samostatné packages.config soubory pro každý projekt?**

Ve většině projektů, kde samostatné projekty žijí v samostatných složkách, to není problém jako NuGet identifikuje `packages.config` soubory v každém projektu. S NuGet 3.3+ a více projektů ve stejné složce, můžete `packages.config` vložit název `packages.{project-name}.config`projektu do názvy souborů použít vzor a NuGet používá tento soubor.

To to není problém při použití PackageReference, jako každý soubor projektu obsahuje vlastní seznam závislostí.

**V seznamu úložišť nevidím nuget.org, jak je získám zpět?**

- Přidejte `https://api.nuget.org/v3/index.json` do seznamu zdrojů nebo
- Odstranit `%appdata%\.nuget\NuGet.Config` (Windows) `~/.nuget/NuGet/NuGet.Config` nebo (Mac/Linux) a nechat NuGet znovu vytvořit.
