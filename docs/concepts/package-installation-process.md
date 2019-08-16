---
title: Co se stane, když se balíček nainstaluje?
description: Podrobné informace o procesu instalace balíčku
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 69ef02e3c935287759b4012aadcfb1cb9811367c
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488448"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>Co se stane, když se nainstaluje balíček NuGet?

Jednoduše řečeno, různé nástroje NuGet obvykle vytvoří odkaz na balíček v souboru projektu nebo `packages.config`a pak provede obnovení balíčku, které efektivně nainstaluje balíček. Výjimkou je `nuget install`, že balíček rozbalí pouze `packages` do složky a neupravuje žádné další soubory.

Obecný postup je následující:

1. (Všechny nástroje s `nuget.exe`výjimkou) zaznamenejte identifikátor a verzi balíčku do souboru projektu `packages.config`nebo.

   Pokud je instalační nástroj sady Visual Studio nebo rozhraní příkazového řádku dotnet, nástroj se nejprve pokusí balíček nainstalovat. Pokud není kompatibilní, balíček se nepřidá do souboru projektu nebo `packages.config`.

2. Získání balíčku:
   - Ověřte, zda je balíček (podle přesně identifikátorem a číslo verze) již nainstalován ve složce *Global-Packages* , jak je popsáno v tématu [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).

   - Pokud balíček není ve složce *Global-Packages* , pokuste se ho načíst ze zdrojů uvedených v [konfiguračních souborech](../consume-packages/Configuring-NuGet-Behavior.md). U online zdrojů se pokuste nejprve načíst balíček z mezipaměti `-NoCache` protokolu HTTP, pokud není zadaný pomocí `nuget.exe` příkazů nebo `--no-cache` je zadaný pomocí `dotnet restore`. (Visual Studio a `dotnet add package` vždy použít mezipaměť.) Pokud se balíček používá z mezipaměti, zobrazí se ve výstupu "mezipaměť". Doba vypršení platnosti mezipaměti je 30 minut.

   - Pokud balíček není v mezipaměti protokolu HTTP, pokuste se ho stáhnout ze zdrojů uvedených v konfiguraci. Pokud se stáhne balíček, ve výstupu se zobrazí zpráva "GET" a "OK". NuGet protokoluje přenosy HTTP při normální podrobností.

   - Pokud balíček nejde úspěšně získat ze všech zdrojů, instalace v tuto chvíli neproběhne s chybou, jako je třeba [NU1103](../reference/errors-and-warnings/NU1103.md). Všimněte si, že `nuget.exe` chyby z příkazů zobrazují jenom poslední vybraný zdroj, ale to znamená, že balíček není dostupný z libovolného zdroje.

   Při získávání balíčku může platit pořadí zdrojů v konfiguraci NuGet:

   - Před kontrolou zdrojů HTTP kontroluje NuGet zdrojové složky a sdílené síťové složky.

3. Uložte kopii balíčku a další informace do složky *mezipaměti HTTP* , jak je popsáno v tématu [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).

4. Při stažení nainstalujte balíček do složky *globálních balíčků* pro jednotlivé uživatele. NuGet vytvoří pro každý identifikátor balíčku podsložku a pak vytvoří podsložky pro každou nainstalovanou verzi balíčku.

5. NuGet nainstaluje závislosti balíčků podle potřeby. Tento proces může aktualizovat verze balíčku v procesu, jak je popsáno v tématu [řešení závislosti](../concepts/dependency-resolution.md).

6. Aktualizovat další soubory a složky projektu:

    - Pro projekty, které používají PackageReference, aktualizujte graf závislosti balíčku `obj/project.assets.json`uložený v. Samotný obsah balíčku se nekopíruje do žádné složky projektu.
    - Aktualizujte `app.config` nebo, Pokudbalíčekpoužívátransformacezdrojovéhoakonfiguračníhosouboru.`web.config` [](../create-packages/source-and-config-file-transformations.md)

7. (Pouze Visual Studio) Zobrazit soubor Readme balíčku, pokud je k dispozici v okně sady Visual Studio.

Využijte své produktivní kódování pomocí balíčků NuGet!
