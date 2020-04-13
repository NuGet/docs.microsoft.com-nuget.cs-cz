---
title: Přehled a pracovní postup používání balíčků NuGet
description: Přehled procesu spotřebovávání balíčků NuGet v projektu s odkazy na jiné konkrétní části procesu.
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: ddd1d163e18ed4ce1e7cbf41ed152acc40c1c423
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428882"
---
# <a name="package-consumption-workflow"></a>Pracovní postup spotřeba balíčků

Mezi nuget.org a soukromými galeriemi balíčků, které by vaše organizace mohla vytvořit, najdete desítky tisíc velmi užitečných balíčků, které můžete používat ve svých aplikacích a službách. Ale bez ohledu na zdroj, náročné balíček následuje stejný obecný pracovní postup.

![Tok jít do zdroje balíčku, najít balíček, instalace v projektu, pak přidání using prohlášení a volání balíčku API](media/Overview-01-GeneralFlow.png)

\*_Visual Studio `dotnet.exe` a pouze. Příkaz `nuget install` nezmění soubory projektu ani `packages.config` soubor; položky musí být spravovány ručně._

Další podrobnosti naleznete [v tématu Hledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md) a Co se [stane, když je balíček nainstalován?](../concepts/package-installation-process.md).

NuGet si pamatuje identitu a číslo verze každého nainstalovaného balíčku a zapisuje jej do souboru projektu (pomocí [PackageReference](../consume-packages/package-references-in-project-files.md)) nebo [`packages.config`](../reference/packages-config.md)v závislosti na typu projektu a verzi NuGet. S NuGet 4.0+, PackageReference je upřednostňována, i když je konfigurovatelný v sadě Visual Studio prostřednictvím [ui Správce balíčků](install-use-packages-visual-studio.md). V každém případě můžete kdykoli vyhledat příslušný soubor a zobrazit úplný seznam závislostí pro váš projekt.

> [!Tip]
> Je rozumné vždy zkontrolovat licenci pro každý balíček, který chcete použít ve svém softwaru. Na nuget.org najdete odkaz **Informace o licenci** na pravé straně stránky s popisem každého balíčku. Pokud balíček nespecifikuje licenční podmínky, obraťte se přímo na vlastníky balíčku pomocí odkazu **Vlastníci kontaktů** na stránce balíčku. Společnost Microsoft vám nelicencuje žádné duševní vlastnictví od poskytovatelů balíčků třetích stran a není odpovědná za informace poskytnuté třetími stranami.

Při instalaci balíčků NuGet obvykle zkontroluje, zda balíček je již k dispozici z mezipaměti. Tuto mezipaměť můžete ručně vymazat z příkazového řádku, jak je popsáno v části [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).

NuGet také zajišťuje, že cílové architektury podporované balíček jsou kompatibilní s projektem. Pokud balíček neobsahuje kompatibilní sestavení, NuGet zobrazí chybu. Viz [Řešení nekompatibilních chyb balíčků](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).

Při přidávání kódu projektu do zdrojového úložiště obvykle nezahrnují balíčky NuGet. Ti, kteří později klonovat úložiště nebo jinak získat projekt, včetně agentů sestavení v systémech, jako je Visual Studio Team Services, musí obnovit potřebné balíčky před spuštěním sestavení:

![Tok obnovení balíčků NuGet klonováním úložiště a použitím příkazu obnovení](media/Overview-02-RestoreFlow.png)

[Nástroj Restore](../consume-packages/package-restore.md) balíčků používá informace `packages.config` v souboru projektu nebo k přeinstalaci všech závislostí. Všimněte si, že existují rozdíly v procesu, jak je popsáno v [řešení závislostí](../concepts/dependency-resolution.md). Výše uvedený diagram také nezobrazuje příkaz obnovení pro konzolu Správce balíčků, protože pokud používáte konzolu, jste již v kontextu sady Visual Studio, která obvykle automaticky obnovuje balíčky a poskytuje příkaz na úrovni řešení, jak je znázorněno.

V některých případě je nutné přeinstalovat balíčky, které jsou již zahrnuty v projektu, který může také přeinstalovat závislosti. To je snadné pomocí `nuget reinstall` příkazu nebo konzoly NuGet Package Manager. Podrobnosti naleznete [v tématu Přeinstalace a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md).

Nakonec chování NuGet je řízen `Nuget.Config` soubory. Více souborů lze centralizovat určitá nastavení na různých úrovních, jak je vysvětleno v [konfiguraci NuGet Chování](../consume-packages/configuring-nuget-behavior.md).

## <a name="ways-to-install-a-nuget-package"></a>Způsoby instalace balíčku NuGet

Balíčky NuGet jsou staženy a nainstalovány pomocí některé z metod v následující tabulce.

| Nástroj | Popis |
| --- | --- |
| [Rozhraní se kontitu dotnet.exe](install-use-packages-dotnet-cli.md) | (Všechny platformy) Nástroj rozhraní CLI pro knihovny .NET Core a .NET Standard a pro projekty ve stylu sady SDK, které cílí na rozhraní .NET Framework (viz [atribut SDK).](/dotnet/core/tools/csproj#additions) Načte balíček \<identifikovaný\> package_name a přidá odkaz na soubor projektu. Také načte a nainstaluje závislosti. |
| Visual Studio | (Windows a Mac) Poskytuje unové nastavení, jehož prostřednictvím můžete procházet, vybírat a instalovat balíčky a jejich závislosti do projektu ze zadaného zdroje balíčku. Přidá odkazy na nainstalované balíčky do souboru projektu.<ul><li>[Instalace a správa balíčků pomocí sady Visual Studio](install-use-packages-visual-studio.md)</li><li>[Zahrnutí balíčku NuGet do projektu (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [Konzola Správce balíčků (Visual Studio)](install-use-packages-powershell.md) | (Pouze windows) Načte a nainstaluje balíček identifikovaný \<package_name\> z vybraného zdroje do zadaného projektu v řešení a potom přidá odkaz na soubor projektu. Také načte a nainstaluje závislosti. |
| [Rozhraní příkazového řádku nuget.exe](install-use-packages-nuget-cli.md) | (Všechny platformy) Nástroj rozhraní CLI pro knihovny rozhraní .NET Framework a projekty, které nejsou ve stylu sady SDK a které cílí na knihovny .NET Standard. Načte balíček \<identifikovaný\> package_name a rozšíří jeho obsah do složky v aktuálním adresáři; můžete také načíst všechny `packages.config` balíčky uvedené v souboru. Také načte a nainstaluje závislosti, ale neprovede `packages.config`žádné změny v souborech projektu nebo . |
