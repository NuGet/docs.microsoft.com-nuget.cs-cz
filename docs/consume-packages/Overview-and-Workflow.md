---
title: Přehled a pracovní postup použití balíčků NuGet
description: Přehled procesu využívání balíčků NuGet v projektu s odkazy na jiné konkrétní části procesu.
author: JonDouglas
ms.author: jodou
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: d1d6df3bcc36d8a78fcee97099b301c9ffc440d9
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323632"
---
# <a name="package-consumption-workflow"></a>Pracovní postup spotřeby balíčku

Mezi nuget.org a soukromými balíčky, které může vaše organizace navázat, najdete desítky tisíců vysoce užitečných balíčků, které můžete použít ve svých aplikacích a službách. Ale bez ohledu na zdroj, spotřeba balíčku se řídí stejným obecným pracovním postupem.

![Postup přechodu na zdroj balíčku, vyhledání balíčku, jeho instalace do projektu a přidání příkazu Using a volání do rozhraní API balíčku](media/Overview-01-GeneralFlow.png)

\*_Pouze Visual Studio a `dotnet.exe` . `nuget install`Příkaz neupraví soubory projektu ani `packages.config` soubor; položky musí být spravovány ručně._

Další podrobnosti najdete v tématu [vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md) a [co se stane, když se balíček nainstaluje?](../concepts/package-installation-process.md).

NuGet si pamatuje identitu a číslo verze každého nainstalovaného balíčku, nahrává ho buď do souboru projektu (pomocí [PackageReference](../consume-packages/package-references-in-project-files.md)), nebo v [`packages.config`](../reference/packages-config.md) závislosti na typu projektu a vaší verzi nugetu. S NuGet 4.0 + je PackageReference upřednostňovaný, i když se to dá nakonfigurovat v aplikaci Visual Studio prostřednictvím [uživatelského rozhraní Správce balíčků](install-use-packages-visual-studio.md). V každém případě se můžete kdykoli podívat na příslušný soubor a zobrazit úplný seznam závislostí pro váš projekt.

> [!Tip]
> Je vhodné vždycky kontrolovat licenci pro každý balíček, který máte v úmyslu používat ve svém softwaru. Na nuget.org najdete odkaz **licenční informace** na pravé straně každé stránky s popisem balíčku. Pokud balíček neurčí licenční smlouvu, obraťte se na vlastníka balíčku přímo pomocí odkazu **vlastníci kontaktu** na stránce balíček. Společnost Microsoft nelicencuje žádné duševní vlastnictví od poskytovatelů balíčků třetích stran a nezodpovídá za informace poskytované třetími stranami.

Při instalaci balíčků NuGet obvykle kontroluje, jestli je balíček už dostupný z jeho mezipaměti. Tuto mezipaměť můžete ručně vymazat z příkazového řádku, jak je popsáno v tématu [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).

NuGet také zajišťuje, aby cílové architektury podporované balíčkem byly kompatibilní s vaším projektem. Pokud balíček neobsahuje kompatibilní sestavení, NuGet zobrazí chybu. Viz [řešení chyb nekompatibilních balíčků](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).

Při přidávání kódu projektu do zdrojového úložiště obvykle nezahrnujete balíčky NuGet. Uživatelé, kteří později naklonují úložiště nebo jinak nastavili projekt, včetně agentů sestavení v systémech, jako je Visual Studio Team Services, musí před spuštěním sestavení obnovit potřebné balíčky:

![Tok obnovování balíčků NuGet klonováním úložiště a pomocí příkazu pro obnovení](media/Overview-02-RestoreFlow.png)

[Obnovení balíčku](../consume-packages/package-restore.md) používá informace v souboru projektu nebo `packages.config` přeinstaluje všechny závislosti. Všimněte si, že v procesu je nějaký rozdíl, jak je popsáno v tématu [řešení závislosti](../concepts/dependency-resolution.md). Kromě toho diagram výše nezobrazuje příkaz Restore pro konzolu Správce balíčků, protože pokud používáte konzolu nástroje, kterou již máte v kontextu sady Visual Studio, která obvykle obnovuje balíčky automaticky a poskytuje příkaz na úrovni řešení, jak je znázorněno na obrázku.

V některých případech je potřeba přeinstalovat balíčky, které už jsou zahrnuté v projektu, což může přeinstalovat i závislosti. To je snadné pomocí `nuget reinstall` příkazu nebo konzoly Správce balíčků NuGet. Podrobnosti najdete v tématu [Přeinstalace a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md).

Nakonec se chování NuGet řídí `NuGet.Config` soubory. Více souborů lze použít k centralizaci určitých nastavení na různých úrovních, jak je vysvětleno v tématu [Konfigurace chování NuGet](../consume-packages/configuring-nuget-behavior.md).

## <a name="ways-to-install-a-nuget-package"></a>Způsoby instalace balíčku NuGet

Balíčky NuGet se stahují a instalují pomocí kterékoli z metod v následující tabulce.

| Nástroj | Platformy | Description |
| --- | --- | --- |
| [dotnet CLI](install-use-packages-dotnet-cli.md) | Vše | Nástroj rozhraní příkazového řádku pro knihovny .NET Core a .NET Standard a pro projekty ve stylu sady SDK, které cílí na .NET Framework (viz [atribut sady SDK](/dotnet/core/tools/csproj#additions)). Načte balíček identifikovaný \<package_name\> a přidá odkaz na soubor projektu. Také načte a nainstaluje závislosti. |
| Visual Studio | Windows a Mac | Poskytuje uživatelské rozhraní, pomocí kterého můžete procházet, vybírat a instalovat balíčky a jejich závislosti do projektu ze zadaného zdroje balíčku. Přidá odkazy na nainstalované balíčky do souboru projektu.<ul><li>[Instalace a Správa balíčků pomocí sady Visual Studio](install-use-packages-visual-studio.md)</li><li>[Zahrnutí balíčku NuGet do projektu (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [Konzola Správce balíčků (Visual Studio)](install-use-packages-powershell.md) | Jen ve Windows | Načte a nainstaluje balíček identifikovaný \<package_name\> z vybraného zdroje do zadaného projektu v řešení a pak přidá odkaz na soubor projektu. Také načte a nainstaluje závislosti. |
| [nuget.exe CLI](install-use-packages-nuget-cli.md) | Vše | Nástroj rozhraní příkazového řádku pro knihovny .NET Framework a projekty, které nejsou ve stylu sady SDK, které cílí na .NET Standard knihovny. Načte balíček identifikovaný \<package_name\> a rozbalí jeho obsah do složky v aktuálním adresáři. může také načíst všechny balíčky uvedené v `packages.config` souboru. Také načte a nainstaluje závislosti, ale neprovede žádné změny v souborech projektu nebo `packages.config` . |
