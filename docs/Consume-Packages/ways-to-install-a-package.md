---
title: Způsoby instalace balíčků NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: overview
ms.prod: nuget
ms.technology: ''
description: Popisuje postup instalace balíčků NuGet do projektu, včetně toho, co se stane, na disku a pro soubory použít projektu.
keywords: Nainstalujte NuGet, využívání balíčku NuGet, instalace balíčků NuGet, odkazy na balíček NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b8cce7bd6c1bd73eb018b8891ddd72b2f4432d55
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>Různé způsoby, jak nainstalovat balíček NuGet

Balíčky NuGet jsou stáhli a nainstalovali pomocí libovolné metody v následující tabulce (najdete v části [nástrojích klienta nainstalovat NuGet](../install-nuget-client-tools.md) Pokud nemáte tyto už nainstalované). Balíček může načítat z mezipaměti místo stáhli.

| Metoda | Popis |
| --- | --- |
| dotnet.exe CLI<br/>`dotnet add package <package_name>` | (Všechny platformy) Načte balíček identifikovaný \<název_balíčku\>, představuje obsah ve složce v aktuálním adresáři a přidá odkaz na soubor projektu. Také načte a nainstaluje závislosti.<ul><li>[Instalace a použití balíčku (rozhraní příkazového řádku dotnet)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[příkaz balíček přidat DotNet.](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| Uživatelského rozhraní Správce balíčků (Visual Studio) | (Windows a Mac) Poskytuje uživatelské rozhraní, pomocí kterého můžete procházet, vyberte a nainstalujte balíčky a jejich závislosti do projektu ze zdroje zadaného balíčku. Přidá odkazy na balíčky nainstalované do souboru projektu.<ul><li>[Instalace a použití balíčku (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Odkaz uživatelského rozhraní Správce balíčků (Windows)](../tools/package-manager-ui.md)</li><li>[Včetně balíček NuGet do projektu (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Konzola správce balíčků (Visual Studio)<br/>`Install-Package <package_name>` | (Jenom Windows) Načte a nainstaluje balíček identifikovaný \<název_balíčku\> z vybraného zdroje do zadaného projektu v řešení, pak přidá odkaz na soubor projektu. Také načte a nainstaluje závislosti.<ul><li>[Instalace a použití balíčku (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Konzola správce balíčků Průvodce](../tools/package-manager-console.md)</li></ul> |
| nuget.exe CLI<br/>`nuget install <package_name>` | (Všechny platformy) Načte balíček identifikovaný \<název_balíčku\> a rozšíří jeho obsah do složky v aktuálním adresáři, můžete také načíst všechny balíčky uvedené v `packages.config` souboru. Také načte a nainstaluje závislosti, ale neprovede žádné změny souborů projektu nebo `packages.config`.<ul><li>[příkaz instalovat](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a>Co se stane, když je balíček nainstalován

Jednoduše řečeno, různých nástrojů NuGet obvykle vytvořit odkaz na balíček v souboru projektu nebo `packages.config`, pak proveďte obnovení balíčků, které efektivně nainstaluje balíček. Jedinou výjimkou je `nuget install`, který pouze rozbalí balíček do `packages` složky a další soubory nedojde ke změně.

Obecný postup je následující:

1. (Všechny nástroje, s výjimkou `nuget.exe`) záznam identifikátor balíčku a verzi do souboru projektu nebo `packages.config`.

1. Získání balíčku:
    - Zkontrolujte, zda balíček (číslem přesný identifikátor a verzi) je již nainstalován v *globální balíčky* složky, jak je popsáno na [správy globální balíčky a složky mezipaměti](managing-the-global-packages-and-cache-folders.md).

    - Pokud není v balíčku *globální balíčky* složky, pokoušejí o načtení ho z uvedených zdrojů uvedených v [konfigurační soubory](Configuring-NuGet-Behavior.md). Pro online zdroje, pokus nejdřív načíst balíček z mezipaměti, pokud `-NoCache` je definován s `nuget.exe` příkazy nebo `--no-cache` je definován s `dotnet restore`. (Visual Studio a `dotnet add package` vždy používání mezipaměti.) Pokud se balíček používá z mezipaměti, se zobrazí ve výstupu "MEZIPAMĚŤ". Mezipaměť obsahuje čas vypršení platnosti 30 minut.

    - Pokud balíček není v mezipaměti, pokusí se ji stáhnout z zdroje uvedené v konfiguraci. Pokud se stáhne balíček, se zobrazí ve výstupu "GET" a "OK".

    - Pokud balíček nebylo možné získat úspěšně ze všech zdrojů, instalace selže v tomto okamžiku s chybou, jako [NU1103](../reference/errors-and-warnings.md#nu1103). Poznámka: tuto chyby ze `nuget.exe` příkazy Zobrazit pouze poslední zdroj zaškrtnuto, ale znamená, že balíček nebyl k dispozici z jakéhokoli zdroje.

    Při získávání balíčku, může nainstalovat pořadí zdrojů v konfiguraci NuGet:
      - Pro projekty formátu PackageReference zkontroluje NuGet místní složky a síťové složky zdroje před zaškrtnutím zdrojů HTTP.
      - U projektů pomocí `packages.config` formátu správy, NuGet používá pořadí zdrojů v konfiguraci. Výjimkou je operace obnovení v takovém případě je ignorováno zdroj řazení a NuGet používá balíček z libovolného zdrojového odpovídá nejdřív.
      - Obecně platí není zvlášť důležité, pořadí, ve kterém NuGet kontroluje zdroje, protože libovolný daný balíček s číslem konkrétní identifikátor a verzi se přesně shodují na jakémkoli zdroji zjistí.

1. (Všechny nástroje, s výjimkou `nuget.exe`) uložit kopii balíčku a další informace v *http mezipaměti* složky, jak je popsáno na [správy globální balíčky a složky mezipaměti](managing-the-global-packages-and-cache-folders.md).

1. Pokud stáhli, nainstalujte balíček do za uživatelem *globální balíčky* složky. Vytvoří podsložky pro každý identifikátor balíčku NuGet a potom vytvoří podsložky pro každou nainstalovanou verzi balíčku.

1. Aktualizace jiných projektu soubory a složky:

    - Pro projekty pomocí PackageReference, aktualizovat graf závislostí balíček uložen v `obj/project.assets.json`. Obsah balíčku sami nebudou zkopírovány do libovolné složky projektu.
    - Pro projekty pomocí `packages.config`, zkopírujte části Rozšířené balíčku, které odpovídají cílový framework projektu na do projektu `packages` složky. (Při použití `nuget install`, celý rozšířené balíčku je zkopírovat, protože `nuget.exe` není zkontrolujte soubory projektu k identifikaci cílové rozhraní.)
    - Aktualizace `app.config` nebo `web.config` Pokud balíček používá [zdroje a konfiguračním souboru transformace](../create-packages/source-and-config-file-transformations.md).

1. Nainstalujte všechny závislosti nižší úrovně, pokud není, který už v projektu. Tento proces může aktualizovat verze balíčku v procesu, jak je popsáno v [řešení závislostí](../consume-packages/dependency-resolution.md).

1. (Jenom pro visual Studio) Zobrazte soubor readme balíčku, pokud je k dispozici, v okně Visual Studio.

## <a name="related-articles"></a>Související články

- [Přehled a pracovní postup spotřeby balíčku](../consume-packages/overview-and-workflow.md)
- [Vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md)
- [Správa složky mezipaměti a globální balíčky NuGet](managing-the-global-packages-and-cache-folders.md)
- [Konfigurace chování NuGetu](../consume-packages/configuring-nuget-behavior.md)
