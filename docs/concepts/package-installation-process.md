---
title: Co se stane, když je balíček nainstalován?
description: Podrobné informace o procesu instalace balíčku
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 1ae030c308b14b8884fb608c1683c8c46000b0bd
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "77036900"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>Co se stane, když je nainstalován balíček NuGet?

Jednoduše řečeno, různé nástroje NuGet obvykle vytvořit odkaz na balíček v souboru projektu nebo `packages.config`potom provést obnovení balíčku, který efektivně nainstaluje balíček. Výjimkou je `nuget install`, která pouze rozbalí `packages` balíček do složky a nezmění žádné jiné soubory.

Obecný postup:

1. (Všechny nástroje `nuget.exe`kromě ) Zaznamenejte identifikátor balíčku a `packages.config`verzi do souboru projektu nebo .

   Pokud je instalačnínástroj Visual Studio nebo dotnet CLI, nástroj se nejprve pokusí nainstalovat balíček. Pokud je nekompatibilní, balíček není přidán do `packages.config`souboru projektu nebo .

2. Získejte balíček:
   - Zkontrolujte, zda je balíček (podle přesného identifikačního čísla a čísla verze) již nainstalován ve složce *globálních balíčků,* jak je popsáno v [části Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).

   - Pokud balíček není ve složce *globální balíčky,* pokuste se jej načíst ze zdrojů uvedených v [konfiguračních souborech](../consume-packages/Configuring-NuGet-Behavior.md). U online zdrojů se nejprve pokuste načíst balíček z mezipaměti HTTP, pokud není `-NoCache` zadán pomocí `nuget.exe` příkazů nebo `--no-cache` není zadán pomocí . `dotnet restore` (Visual Studio `dotnet add package` a vždy používat mezipaměť.) Pokud je balíček použit z mezipaměti, "CACHE" se zobrazí ve výstupu. Mezipaměť má dobu vypršení platnosti 30 minut.

   - Pokud balíček není v mezipaměti HTTP, pokuste se jej stáhnout ze zdrojů uvedených v konfiguraci. Pokud je balíček stažen, "GET" a "OK" se objeví ve výstupu. NuGet protokoly http přenosy na normální podrobnost.

   - Pokud balíček nelze úspěšně získat z žádného zdroje, instalace se nezdaří v tomto okamžiku s chybou, jako je [nu1103](../reference/errors-and-warnings/NU1103.md). Všimněte si, že chyby z `nuget.exe` příkazů zobrazit pouze poslední zdroj zaškrtnuto, ale znamená, že balíček nebyl k dispozici z žádného zdroje.

   Při získávání balíčku může použít pořadí zdrojů v konfiguraci NuGet:

   - NuGet kontroluje zdroje místních složek a síťových sdílených složek před kontrolou zdrojů HTTP.

3. Uložte kopii balíčku a další informace do složky *http-cache,* jak je popsáno v [části Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).

4. Pokud je stažen, nainstalujte balíček do složky *globálních balíčků* pro jednotlivé uživatele. NuGet vytvoří podsložku pro každý identifikátor balíčku, pak vytvoří podsložky pro každou nainstalovanou verzi balíčku.

5. NuGet nainstaluje závislosti balíčků podle potřeby. Tento proces může aktualizovat verze balíčků v procesu, jak je popsáno v [řešení závislostí](../concepts/dependency-resolution.md).

6. Aktualizace dalších souborů a složek projektu:

    - U projektů používajících odkaz packagereference aktualizujte graf závislostí balíčku uložený v aplikaci `obj/project.assets.json`. Samotný obsah balíčku nejsou zkopírovány do žádné složky projektu.
    - Aktualizace `app.config` a/nebo `web.config` pokud balíček používá [transformace zdrojového a konfiguračního souboru](../create-packages/source-and-config-file-transformations.md).

7. (Pouze visual studio) Zobrazení souboru readme balíčku, pokud je k dispozici, v okně sady Visual Studio.

Užijte si produktivní kódování s balíčky NuGet!
