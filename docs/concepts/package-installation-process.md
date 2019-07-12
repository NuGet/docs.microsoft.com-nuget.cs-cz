---
title: Co se stane, když je nainstalován balíček?
description: Podrobné informace o procesu instalace balíčku
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 5676239bedb7f8fbe9f74725864afd297405d5c1
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842331"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>Co se stane při instalaci balíčku NuGet?

Jednoduše ale nutné dodat, jiné nástroje NuGet obvykle vytvořit odkaz na balíček v souboru projektu nebo `packages.config`, proveďte obnovení balíčků, což účinně nainstaluje balíček. Výjimkou je `nuget install`, který pouze rozbalí balíček do `packages` složky a nezmění žádné další soubory.

Obecný postup je následující:

1. (Všechny nástroje, s výjimkou `nuget.exe`) identifikátor balíčku a verzi si poznamenejte do souboru projektu nebo `packages.config`.

   Pokud je nástroj pro instalaci sady Visual Studio nebo rozhraní příkazového řádku dotnet, nástroj nejdřív pokusí nainstalovat balíček. Pokud se jedná o nekompatibilní, balíček není přidán do souboru projektu nebo `packages.config`.

2. Získejte balíček:
   - Zkontrolujte, jestli balíček (číslem přesný identifikátor a verzi) je už nainstalovaná v *global-packages* složky, jak je popsáno na [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).

   - Pokud balíček není v *global-packages* složky, pokus o načtení z uvedené zdroje podle [konfigurační soubory](../consume-packages/Configuring-NuGet-Behavior.md). Pro online zdroje pokusí nejprve balíček načíst z mezipaměti HTTP, není-li `-NoCache` zadán s parametrem `nuget.exe` příkazy nebo `--no-cache` zadán s parametrem `dotnet restore`. (Visual Studio a `dotnet add package` vždy používat mezipaměť.) Pokud je balíček z mezipaměti, se zobrazí ve výstupu "Mezipaměti". Mezipaměť obsahuje dobu vypršení platnosti 30 minut.

   - Pokud balíček není v mezipaměti protokolu HTTP, pokuste se ho stáhnout z uvedené v konfiguraci zdroje. Pokud se stáhne balíček ve výstupu se zobrazí "GET" a "OK". NuGet protokoly provozu http na normální podrobností.

   - Pokud balíček nelze úspěšně získat ze všech zdrojů, instalace se nezdaří v tuto chvíli s chybou jako [NU1103](../reference/errors-and-warnings/NU1103.md). Poznámka: tuto chyby z `nuget.exe` zobrazit příkazy pouze poslední zdroje zaškrtnuto, ale znamená, že balíček nebyl dostupný z libovolného zdroje.

   Při získávání balíčku, může použít zdroje v konfiguraci Nugetu pořadí:

   - NuGet kontroluje zdroje místní složky a síťové sdílené složky, před vrácením zdrojů HTTP.

3. Uložit kopii balíčku a další informace *http-cache* složky, jak je popsáno na [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).

4. Pokud si stáhli, nainstalujte balíček do jednotlivé uživatele *global-packages* složky. NuGet vytvoří podsložky pro každý identifikátor balíčku a programu vytváří podsložky pro každou nainstalovanou verzi balíčku.

5. Závislosti balíčků NuGet nainstaluje podle potřeby. Tento proces může aktualizovat verze balíčku v procesu, jak je popsáno v [řešení závislostí](../consume-packages/dependency-resolution.md).

6. Aktualizace dalších projektových souborů a složek:

    - Pro projekty pomocí PackageReference, aktualizace uložených v grafu závislostí balíčku `obj/project.assets.json`. Balíček obsahu nejsou zkopírovány do libovolné složky projektu.
    - Aktualizace `app.config` a/nebo `web.config` pokud používá balíček [zdrojových a konfiguračních souborů transformace](../create-packages/source-and-config-file-transformations.md).

7. (Pouze visual Studio) Zobrazte soubor readme balíčku, pokud je k dispozici v okně aplikace Visual Studio.

Užijte si produktivní psaní kódu s balíčky NuGet.
