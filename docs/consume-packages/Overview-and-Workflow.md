---
title: Přehled a pracovní postup pomocí balíčků NuGet
description: Přehled procesu využívání balíčků NuGet v projektu, s odkazy na další konkrétní části procesu.
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: 506a093ff4d62c10c896246f746e6765f64f33f4
ms.sourcegitcommit: a801052aa728a3a137225ca3ef3ff89f2d1c6b76
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/18/2019
ms.locfileid: "54403161"
---
# <a name="package-consumption-workflow"></a>Spotřeba zabalit pracovní postup

Mezi nuget.org a privátní balíček galerie, které vaše organizace může vytvořit najdete desítky tisíc balíčků velmi užitečné pro použití ve vašich aplikacích a službách. Ale bez ohledu na zdroj, spotřebovává balíček následuje stejný obecný pracovní postup.

![Tok přejdete ke zdroji balíčku, vyhledání balíčku, instalace v projektu a přidání pomocí příkazu a volání rozhraní API balíčku](media/Overview-01-GeneralFlow.png)

\* _Visual Studio a `dotnet.exe` pouze. `nuget install` Příkaz neprovede žádné změny soubory projektu nebo `packages.config` soubor; položky se musí spravovat ručně._

Další podrobnosti najdete v tématu [hledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md) a [různých způsobů, jak nainstalovat balíček NuGet](ways-to-install-a-package.md).

NuGet si pamatuje identity a verze počet každý nainstalovaný balíček nahrávání buď [ `packages.config` ](../reference/packages-config.md) nebo soubor projektu (pomocí [PackageReference](../consume-packages/package-references-in-project-files.md)), v závislosti na typu projektu a verze balíčku nuget. Nuget 4.0 +, PackageReference upřednostňována, i když je to možnost konfigurace v sadě Visual Studio prostřednictvím [možnosti uživatelského rozhraní Správce balíčků](../tools/package-manager-ui.md). V každém případě můžete prohlédnout v souboru příslušné kdykoli chcete zobrazit úplný seznam závislostí pro váš projekt.

> [!Tip]
> Je vhodné vždy zkontrolujte licence pro každý balíček, který chcete používat váš software. Na nuget.org, můžete najít **informace o licenci** odkaz na pravé straně stránky popis každého balíčku. Pokud balíček nejsou zadány licenční podmínky, obraťte se přímo pomocí vlastníka balíčku **obraťte se na vlastníky** odkaz na stránce balíček. Společnost Microsoft není licence duševního vlastnictví, od poskytovatelů třetích stran balíček a neodpovídá za informace, které jsou poskytovány třetími stranami.

Při instalaci balíčků NuGet obvykle zkontroluje, jestli tento balíček již k dispozici uloženou v mezipaměti. Můžete ručně vymazat tuto mezipaměť z příkazového řádku, jak je popsáno na [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).

NuGet také zajišťuje, že jsou kompatibilní s vaším projektem cílových platforem podporovaných balíček. Pokud balíček neobsahuje kompatibilní sestavení, NuGet zobrazí chybu. Zobrazit [řešení chyb nekompatibilní balíček](dependency-resolution.md#resolving-incompatible-package-errors).

Při přidávání projektu kódu do úložiště zdrojového kódu, obvykle neobsahuje balíčky NuGet. Uživatele, kteří později naklonujte úložiště nebo jinak získají projektu, včetně agentů sestavení na systémech, jako je Visual Studio Team Services, musíte obnovit potřebné balíčky před spuštěním sestavení:

![Obnovují se balíčky NuGet tak, že klonování úložiště a pomocí příkazu restore tok](media/Overview-02-RestoreFlow.png)

[Obnovení balíčků](../consume-packages/package-restore.md) používá informace v souboru projektu nebo `packages.config` přeinstalovat všechny závislosti. Všimněte si, že existují rozdíly v procesu používané, jak je popsáno v [řešení závislostí](../consume-packages/dependency-resolution.md). Navíc výše uvedeném diagramu nezobrazí příkaz restore pro konzolu Správce balíčků vzhledem k tomu, že pokud jste s konzolou jste již v rámci sady Visual Studio, která obvykle automaticky obnoví balíčky a poskytuje řešení úrovni příkaz jako Zobrazit.

Někdy je potřeba znovu nainstaluje balíčky, které už jsou obsažené v projektu, který může také znovu nainstalovat závislosti. Je to snadné dosáhnout pomocí `nuget reinstall` příkaz nebo konzoly Správce balíčků NuGet. Podrobnosti najdete v tématu [Reinstalling a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md).

Nakonec doprovází chování Nugetu `Nuget.Config` soubory. Více souborů umožňuje centralizovat určitá nastavení na různých úrovních, jak je vysvětleno v [konfigurace chování Nugetu](../consume-packages/configuring-nuget-behavior.md).

Užijte si produktivní psaní kódu s balíčky NuGet.
