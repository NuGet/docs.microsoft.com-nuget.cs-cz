---
title: Způsoby instalace balíčků NuGet
description: Popisuje postup instalace balíčků NuGet do projektu, včetně toho, co se stane, na disk a do souborů projektu použít.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/12/2018
ms.topic: overview
ms.openlocfilehash: 0f59c3b7f1e32ae34889921c13d15074ef5c1260
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843378"
---
# <a name="different-ways-to-install-a-nuget-package"></a>Různé způsoby instalace balíčku NuGet

Balíčky NuGet se stáhnout a nainstalovat pomocí některé z metod v následující tabulce (naleznete v tématu [klientských nástrojů Nugetu nainstalovat](../install-nuget-client-tools.md) Pokud nemáte k dispozici tyto nainstalovaná). Balíček může načítat z mezipaměti namísto stáhli.

| Metoda | Popis |
| --- | --- |
| dotnet.exe CLI<br/>`dotnet add package <package_name>` | (Všechny platformy) Načte balíček identifikovaný \<název_balíčku\>svůj obsah rozbalí do složky v aktuálním adresáři a přidá odkaz na soubor projektu. Také načte a nainstaluje závislosti.<ul><li>[Instalace a použití balíčku (rozhraní příkazového řádku dotnet)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[příkaz DotNet add příkaz balíčku](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| Uživatelské rozhraní Správce balíčků (Visual Studio) | (Windows a Mac) Poskytuje uživatelské rozhraní, která můžete procházet, vybrat a nainstalovat balíčky a jejich závislosti do projektu ze zdroje zadaného balíčku. Přidá odkazy na balíčky nainstalované do souboru projektu.<ul><li>[Instalace a použití balíčku (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Reference k uživatelskému rozhraní Správce balíčků (Windows)](../tools/package-manager-ui.md)</li><li>[Zahrnutí balíčku NuGet do projektu (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Konzola správce balíčků (Visual Studio)<br/>`Install-Package <package_name>` | (Jenom Windows) Načte a nainstaluje balíček identifikovaný \<název_balíčku\> z vybraného zdroje do zadaného projektu v řešení, přidá odkaz na soubor projektu. Také načte a nainstaluje závislosti.<ul><li>[Instalace a použití balíčku (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Průvodce Konzola správce balíčků](../tools/package-manager-console.md)</li></ul> |
| rozhraní příkazového řádku nuget.exe<br/>`nuget install <package_name>` | (Všechny platformy) Načte balíček identifikovaný \<název_balíčku\> a rozšíří jeho obsah do složky v aktuálním adresáři, můžete také načíst všechny balíčky uvedené v `packages.config` souboru. Také načte a nainstaluje závislosti, ale neprovede žádné změny do souborů projektu nebo `packages.config`.<ul><li>[příkaz instalovat](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a>Co se stane, když je nainstalován balíček

Jednoduše ale nutné dodat, jiné nástroje NuGet obvykle vytvořit odkaz na balíček v souboru projektu nebo `packages.config`, proveďte obnovení balíčků, což účinně nainstaluje balíček. Výjimkou je `nuget install`, který pouze rozbalí balíček do `packages` složky a nezmění žádné další soubory.

Obecný postup je následující:

1. (Všechny nástroje, s výjimkou `nuget.exe`) identifikátor balíčku a verzi si poznamenejte do souboru projektu nebo `packages.config`.

2. Získejte balíček:
   - Zkontrolujte, jestli balíček (číslem přesný identifikátor a verzi) je už nainstalovaná v *global-packages* složky, jak je popsáno na [Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md).

   - Pokud balíček není v *global-packages* složky, pokus o načtení z uvedené zdroje podle [konfigurační soubory](Configuring-NuGet-Behavior.md). Pro online zdroje pokusí nejprve balíček načíst z mezipaměti, není-li `-NoCache` zadán s parametrem `nuget.exe` příkazy nebo `--no-cache` zadán s parametrem `dotnet restore`. (Visual Studio a `dotnet add package` vždy používat mezipaměť.) Pokud je balíček z mezipaměti, se zobrazí ve výstupu "Mezipaměti". Mezipaměť obsahuje dobu vypršení platnosti 30 minut.

   - Pokud balíček není v mezipaměti, pokuste se ho stáhnout z uvedené v konfiguraci zdroje. Pokud se stáhne balíček ve výstupu se zobrazí "GET" a "OK".

   - Pokud balíček nelze úspěšně získat ze všech zdrojů, instalace se nezdaří v tuto chvíli s chybou jako [NU1103](../reference/errors-and-warnings/NU1103.md). Poznámka: tuto chyby z `nuget.exe` zobrazit příkazy pouze poslední zdroje zaškrtnuto, ale znamená, že balíček nebyl dostupný z libovolného zdroje.

   Při získávání balíčku, může použít zdroje v konfiguraci Nugetu pořadí:

   - Pro projekty ve formátu PackageReference zkontroluje NuGet místní složky a síťové složky zdroje před vrácením zdrojů HTTP.

   - Pro projekty používající `packages.config` formátu správy NuGet používá pořadí zdrojů v konfiguraci. Výjimkou je operace obnovení v takovém případě se ignoruje řazení zdroje a NuGet používá balíček ze zdroje podle toho, která odpovídá nejdřív.

   - Pořadí, ve kterém NuGet kontroluje zdrojů není obecně platí, zejména smysluplné, protože libovolný daný balíček s konkrétní identifikátor a verzi číslo je přesně tatáž na libovolné zdroj se nenašel.

3. (Všechny nástroje, s výjimkou `nuget.exe`) uložit kopii balíčku a další informace *http-cache* složky, jak je popsáno na [Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md).

4. Pokud si stáhli, nainstalujte balíček do jednotlivé uživatele *global-packages* složky. NuGet vytvoří podsložky pro každý identifikátor balíčku a programu vytváří podsložky pro každou nainstalovanou verzi balíčku.

5. Aktualizace dalších projektových souborů a složek:

    - Pro projekty pomocí PackageReference, aktualizace uložených v grafu závislostí balíčku `obj/project.assets.json`. Balíček obsahu nejsou zkopírovány do libovolné složky projektu.
    - Pro projekty používající `packages.config`, zkopírujte tyto části Rozšířené balíčku, které odpovídají cílové rozhraní projektu do projektu `packages` složky. (Při použití `nuget install`, je zkopírovat celý balíček rozšířené, protože `nuget.exe` nezkoumá soubory projektu k identifikaci cílové rozhraní.)
    - Aktualizace `app.config` a/nebo `web.config` pokud používá balíček [zdrojových a konfiguračních souborů transformace](../create-packages/source-and-config-file-transformations.md).

6. Nainstaluje všechny případné závislosti nižší úrovně, pokud není již k dispozici v projektu. Tento proces může aktualizovat verze balíčku v procesu, jak je popsáno v [řešení závislostí](../consume-packages/dependency-resolution.md).

7. (Pouze visual Studio) Zobrazte soubor readme balíčku, pokud je k dispozici v okně aplikace Visual Studio.

## <a name="related-articles"></a>Související články

- [Přehled a pracovní postup využití balíčků](../consume-packages/overview-and-workflow.md)
- [Vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md)
- [Správa složky mezipaměti a globálních balíčků NuGet](managing-the-global-packages-and-cache-folders.md)
- [Konfigurace chování NuGetu](../consume-packages/configuring-nuget-behavior.md)
