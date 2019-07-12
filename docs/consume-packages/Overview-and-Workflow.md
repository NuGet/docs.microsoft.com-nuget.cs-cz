---
title: Přehled a pracovní postup pomocí balíčků NuGet
description: Přehled procesu využívání balíčků NuGet v projektu, s odkazy na další konkrétní části procesu.
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: 4cfc2fde08b240288851b87a391dc42c1ac8ecaf
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842323"
---
# <a name="package-consumption-workflow"></a>Spotřeba zabalit pracovní postup

Mezi nuget.org a privátní balíček galerie, které vaše organizace může vytvořit najdete desítky tisíc balíčků velmi užitečné pro použití ve vašich aplikacích a službách. Ale bez ohledu na zdroj, spotřebovává balíček následuje stejný obecný pracovní postup.

![Tok přejdete ke zdroji balíčku, vyhledání balíčku, instalace v projektu a přidání pomocí příkazu a volání rozhraní API balíčku](media/Overview-01-GeneralFlow.png)

\* _Visual Studio a `dotnet.exe` pouze. `nuget install` Příkaz neprovede žádné změny soubory projektu nebo `packages.config` soubor; položky se musí spravovat ručně._

Další podrobnosti najdete v tématu [hledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md) a [co se stane, když je nainstalován balíček?](../concepts/package-installation-process.md).

NuGet si pamatuje identity a verze počet každý nainstalovaný balíček záznam v jednom souboru projektu (pomocí [PackageReference](../consume-packages/package-references-in-project-files.md)) nebo [ `packages.config` ](../reference/packages-config.md), v závislosti na typu projektu a verze balíčku nuget. Nuget 4.0 +, PackageReference upřednostňována, i když je to možnost konfigurace v sadě Visual Studio prostřednictvím [uživatelské rozhraní Správce balíčků](../tools/package-manager-ui.md). V každém případě můžete prohlédnout v souboru příslušné kdykoli chcete zobrazit úplný seznam závislostí pro váš projekt.

> [!Tip]
> Je vhodné vždy zkontrolujte licence pro každý balíček, který chcete používat váš software. Na nuget.org, můžete najít **informace o licenci** odkaz na pravé straně stránky popis každého balíčku. Pokud balíček nejsou zadány licenční podmínky, obraťte se přímo pomocí vlastníka balíčku **obraťte se na vlastníky** odkaz na stránce balíček. Společnost Microsoft není licence duševního vlastnictví, od poskytovatelů třetích stran balíček a neodpovídá za informace, které jsou poskytovány třetími stranami.

Při instalaci balíčků NuGet obvykle zkontroluje, jestli tento balíček již k dispozici uloženou v mezipaměti. Můžete ručně vymazat tuto mezipaměť z příkazového řádku, jak je popsáno na [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).

NuGet také zajišťuje, že jsou kompatibilní s vaším projektem cílových platforem podporovaných balíček. Pokud balíček neobsahuje kompatibilní sestavení, NuGet zobrazí chybu. Zobrazit [řešení chyb nekompatibilní balíček](dependency-resolution.md#resolving-incompatible-package-errors).

Při přidávání projektu kódu do úložiště zdrojového kódu, obvykle neobsahuje balíčky NuGet. Uživatele, kteří později naklonujte úložiště nebo jinak získají projektu, včetně agentů sestavení na systémech, jako je Visual Studio Team Services, musíte obnovit potřebné balíčky před spuštěním sestavení:

![Obnovují se balíčky NuGet tak, že klonování úložiště a pomocí příkazu restore tok](media/Overview-02-RestoreFlow.png)

[Obnovení balíčků](../consume-packages/package-restore.md) používá informace v souboru projektu nebo `packages.config` přeinstalovat všechny závislosti. Všimněte si, že existují rozdíly v procesu používané, jak je popsáno v [řešení závislostí](../consume-packages/dependency-resolution.md). Navíc výše uvedeném diagramu nezobrazí příkaz restore pro konzolu Správce balíčků vzhledem k tomu, že pokud jste s konzolou jste již v rámci sady Visual Studio, která obvykle automaticky obnoví balíčky a poskytuje řešení úrovni příkaz jako Zobrazit.

Někdy je potřeba znovu nainstaluje balíčky, které už jsou obsažené v projektu, který může také znovu nainstalovat závislosti. Je to snadné dosáhnout pomocí `nuget reinstall` příkaz nebo konzoly Správce balíčků NuGet. Podrobnosti najdete v tématu [Reinstalling a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md).

Nakonec doprovází chování Nugetu `Nuget.Config` soubory. Více souborů umožňuje centralizovat určitá nastavení na různých úrovních, jak je vysvětleno v [konfigurace chování Nugetu](../consume-packages/configuring-nuget-behavior.md).

## <a name="ways-to-install-a-nuget-package"></a>Způsoby, jak nainstalovat balíček NuGet

Balíčky NuGet se stáhnout a nainstalovat pomocí některé z metod v následující tabulce.

| Nástroj | Popis |
| --- | --- |
| [dotnet.exe CLI](install-use-packages-dotnet-cli.md) | (Všechny platformy) Nástroje rozhraní příkazového řádku pro knihovny .NET Core a .NET Standard a sady SDK – vizuální styl projekty, které cílí na rozhraní .NET Framework (viz [SDK atribut](/dotnet/core/tools/csproj#additions)). Načte balíček identifikovaný \<název_balíčku\> a přidá odkaz na soubor projektu. Také načte a nainstaluje závislosti. |
| Visual Studio | (Windows a Mac) Poskytuje uživatelské rozhraní, která můžete procházet, vybrat a nainstalovat balíčky a jejich závislosti do projektu ze zdroje zadaného balíčku. Přidá odkazy na balíčky nainstalované do souboru projektu.<ul><li>[Instalace a Správa balíčků s využitím sady Visual Studio](../tools/package-manager-ui.md)</li><li>[Zahrnutí balíčku NuGet do projektu (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [Konzola správce balíčků v sadě Visual Studio](../tools/package-manager-console.md) | (Jenom Windows) Načte a nainstaluje balíček identifikovaný \<název_balíčku\> z vybraného zdroje do zadaného projektu v řešení, přidá odkaz na soubor projektu. Také načte a nainstaluje závislosti. |
| [nuget.exe CLI](install-use-packages-dotnet-cli.md) | (Všechny platformy) Nástroj příkazového řádku pro knihovny rozhraní .NET Framework a sady SDK styl projekty, které cílit na knihovny .NET Standard. Načte balíček identifikovaný \<název_balíčku\> a rozšíří jeho obsah do složky v aktuálním adresáři, můžete také načíst všechny balíčky uvedené v `packages.config` souboru. Také načte a nainstaluje závislosti, ale neprovede žádné změny do souborů projektu nebo `packages.config`. |
