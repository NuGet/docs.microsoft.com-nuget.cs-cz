---
title: Co se stane, když se balíček nainstaluje?
description: Podrobné informace o procesu instalace balíčku
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 634c421499b06f6b62d88a95f8703614dec5ace8
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699761"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>Co se stane, když se nainstaluje balíček NuGet?

Jednoduše řečeno, různé nástroje NuGet obvykle vytvoří odkaz na balíček v souboru projektu nebo a `packages.config` pak provede obnovení balíčku, které efektivně nainstaluje balíček. Výjimkou je `nuget install` , že balíček rozbalí pouze do `packages` složky a neupravuje žádné další soubory.

Obecný postup:

1. (Všechny nástroje kromě `nuget.exe` ) Poznamenejte si identifikátor a verzi balíčku do souboru projektu nebo `packages.config` .

   Pokud je instalační nástroj sady Visual Studio nebo rozhraní příkazového řádku dotnet, nástroj se nejprve pokusí balíček nainstalovat. Pokud není kompatibilní, balíček se nepřidá do souboru projektu nebo `packages.config` .

2. Získání balíčku:
   - Ověřte, zda je balíček (podle přesně identifikátorem a číslo verze) již nainstalován ve složce *Global-Packages* , jak je popsáno v tématu [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).

   - Pokud balíček není ve složce *Global-Packages* , pokuste se ho načíst ze zdrojů uvedených v [konfiguračních souborech](../consume-packages/Configuring-NuGet-Behavior.md). U online zdrojů se pokuste nejprve načíst balíček z mezipaměti protokolu HTTP, pokud `-NoCache` není zadaný pomocí `nuget.exe` příkazů nebo `--no-cache` je zadaný pomocí `dotnet restore` . (Visual Studio a `dotnet add package` vždy použít mezipaměť.) Pokud se balíček používá z mezipaměti, zobrazí se ve výstupu "mezipaměť". Doba vypršení platnosti mezipaměti je 30 minut.

   - Pokud byl balíček zadán pomocí [plovoucí verze](../consume-packages/Package-References-in-Project-Files.md#floating-versions)nebo bez minimální verze, NuGet *se* spojí se všemi zdroji, aby bylo možné zjistit nejlepší shodu.
   Příklad: `1.*` , `(, 2.0.0]` .

   - Pokud balíček není v mezipaměti protokolu HTTP, pokuste se ho stáhnout ze zdrojů uvedených v konfiguraci. Pokud se stáhne balíček, ve výstupu se zobrazí zpráva "GET" a "OK". NuGet protokoluje přenosy HTTP při normální podrobností.

   - Pokud balíček nejde úspěšně získat ze všech zdrojů, instalace v tuto chvíli neproběhne s chybou, jako je třeba [NU1103](../reference/errors-and-warnings/NU1103.md). Všimněte si, že chyby z `nuget.exe` příkazů zobrazují jenom poslední vybraný zdroj, ale to znamená, že balíček není dostupný z libovolného zdroje.

   Při získávání balíčku může platit pořadí zdrojů v konfiguraci NuGet:

   - Před kontrolou zdrojů HTTP kontroluje NuGet zdrojové složky a sdílené síťové složky.

3. Uložte kopii balíčku a další informace do složky *mezipaměti HTTP* , jak je popsáno v tématu [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).

4. Při stažení nainstalujte balíček do složky *globálních balíčků* pro jednotlivé uživatele. NuGet vytvoří pro každý identifikátor balíčku podsložku a pak vytvoří podsložky pro každou nainstalovanou verzi balíčku.

5. NuGet nainstaluje závislosti balíčků podle potřeby. Tento proces může aktualizovat verze balíčku v procesu, jak je popsáno v tématu [řešení závislosti](../concepts/dependency-resolution.md).

6. Aktualizovat další soubory a složky projektu:

    - Pro projekty, které používají PackageReference, aktualizujte graf závislosti balíčku uložený v `obj/project.assets.json` . Samotný obsah balíčku se nekopíruje do žádné složky projektu.
    - Aktualizujte nebo, `app.config` `web.config` Pokud balíček používá [transformace zdrojového a konfiguračního souboru](../create-packages/source-and-config-file-transformations.md).

7. (Pouze Visual Studio) Zobrazit soubor Readme balíčku, pokud je k dispozici v okně sady Visual Studio.

Využijte své produktivní kódování pomocí balíčků NuGet!
