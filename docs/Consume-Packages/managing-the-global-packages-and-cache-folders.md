---
title: Jak spravovat globální balíčky, mezipaměť, dočasné složky v NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Jak spravovat globální balíček instalační složku, do mezipaměti balíček a dočasné složky, které existují v počítači, které se použijí při instalaci, obnovení a aktualizaci balíčků.
keywords: Globální NuGet balíčky složky, mezipaměti balíčku NuGet, ukládání do mezipaměti balíčku, balíčku instalační složku, mezipaměti NuGet, Správa mezipaměti, místní mezipaměti NuGet, globální mezipaměti NuGet, místní hodnoty – příkaz NuGet, vymazání mezipaměti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e9f4383a3f1700b96e3d6fe9ea4c0a7c24daa45a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Správa globální balíčky, mezipaměti a dočasné složky

Vždy, když instalace, aktualizace nebo obnovení balíčku NuGet spravuje balíčky a informací o balíčku v několika složkách mimo strukturu projektu:

| Název | Popis a umístění (na uživatele)|
| --- | --- |
| global&#8209;packages | *Globální balíčky* složka je, kde NuGet nainstaluje všechny staženého balíčku. Každý balíček je plně rozšířit do podsložky, která odpovídá identifikátor balíčku a číslo verze. Projektů pomocí PackageReference formátu vždy balíčky pro použití přímo z této složky. Při použití `packages.config`, balíčky instalují *globální balíčky* složky, poté zkopírovat do projektu `packages` složky.<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>Přepsat pomocí proměnné prostředí NUGET_PACKAGES `globalPackagesFolder` nebo `repositoryPath` [nastavení konfigurace](../reference/nuget-config-file.md#config-section) (při použití PackageReference a `packages.config`, v uvedeném pořadí), nebo `RestorePackagesPath` nástroje MSBuild vlastnost (MSBuild pouze). Proměnné prostředí mají přednost před nastavením konfigurace.</li></ul> |
| http&#8209;cache | Správce balíčků Visual Studio (NuGet 3.x+) a `dotnet` nástroj úložiště kopie stažených balíčků do mezipaměti, (Uložit jako `.dat` soubory), jsou uspořádány do podsložek pro jednotlivé zdroje balíčku. Balíčky nejsou rozšířit a mezipaměť obsahuje čas vypršení platnosti 30 minut.<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>Přepište pomocí proměnné prostředí NUGET_HTTP_CACHE_PATH.</li></ul> |
| dočasné | Do složky, kde NuGet ukládá dočasné soubory během jeho různé operace.<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |

> [!Note]
> NuGet 3.5 a starší používá *balíčky mezipaměti* místo *http mezipaměti*, který se nachází v `%localappdata%\NuGet\Cache`.

Pomocí mezipaměti a *globální balíčky* složek, NuGet obecně zabraňuje stahovali balíčky, které již existují na počítači, zvýšení výkonu instalaci, aktualizaci a operace obnovení. Při použití PackageReference, *globální balíčky* složky také zabraňuje zachování stažené balíčky v projektu složky, kde se může nechtěně zařadí do správy zdrojového kódu a snižuje NuGet celkového vlivu na počítači úložiště.

Když se zobrazí dotaz pro načtení balíčku, NuGet nejprve hledá v *globální balíčky* složky. Pokud není přesnou verzi balíčku, NuGet kontroluje všechny zdroje balíčků jiným protokolem než HTTP. Pokud stále nebyl nalezen balíček, NuGet hledá balíčku *http mezipaměti* nezadáte `--no-cache` s `dotnet.exe` příkazy nebo `-NoCache` s `nuget.exe` příkazy. Pokud balíček není v mezipaměti, nebo do mezipaměti se nepoužívá, NuGet potom načte balíček přes protokol HTTP.

Další informace najdete v tématu [co se stane, když je nainstalován balíček](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).

## <a name="viewing-folder-locations"></a>Umístění složek pro zobrazení.

Můžete zobrazit pomocí umístění složek [příkaz místní hodnoty – nuget dotnet](/dotnet/core/tools/dotnet-nuget-locals):

```cli
dotnet nuget locals all --list
```

Typické výstup (Mac/Linux; aktuální uživatelské jméno je "uživatel1"):

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
```

Chcete-li zobrazit umístění jednotlivých složek, použijte `http-cache`, `global-packages`, nebo `temp` místo `all`. 

Můžete také zobrazit umístění pomocí [příkaz místní hodnoty – nuget](../tools/cli-ref-locals.md):

```cli
# Display locals for all folders: global-packages, cache, and temp
nuget locals all -list
```

Typické výstup (Windows; aktuální uživatelské jméno je "uživatel1"):

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
```

(`package-cache` se používá v NuGet 2.x a zobrazí se s NuGet 3.5 a starší.)

## <a name="clearing-local-folders"></a>Vymazání místní složky

Pokud dojde k potížím instalace balíčku nebo jinak potřeba zajistit, že instalujete balíčky ze vzdáleného galerie, použijte `locals --clear` možnost (dotnet.exe) nebo `locals -clear` (nuget.exe), zadání složky, které chcete vymazat, nebo `all` na Zrušte zaškrtnutí políčka všechny složky:

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

Všechny balíčky používané projekty, které jsou právě otevřeny v sadě Visual Studio nejsou vymazána z *globální balíčky* složky.

V sadě Visual Studio, použijte **nástroje > Správce balíčků NuGet > Nastavení správce balíčků** nabídky příkazu a pak vyberte **zrušte všechny Cache(s) NuGet**. Správa mezipaměti není v současné době dostupná přes konzolu Správce balíčků.

![Příkaz NuGet možnost pro vymazání mezipaměti](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Řešení potíží s chybami

Následující chyby může stát při použití `nuget locals` nebo `dotnet nuget locals`:

- *Chyba: Proces nemá přístup k souboru <package> vzhledem k tomu, že je stále používán jiným procesem* nebo *vymazání místních prostředků se nezdařilo: nelze odstranit jeden nebo více souborů*

    Jeden nebo více souborů ve složce je používán jiným procesem; Otevřete, který odkazuje na balíčky v projektu sady Visual Studio je například *globální balíčky* složky. Zavřete tyto procesy a zkuste to znovu.

- *Chyba: Přístup k cestě <path> byl odepřen* nebo *adresář není prázdná*

    Nemáte oprávnění k odstranění souborů v mezipaměti. Změnit oprávnění složky, pokud je to možné a akci opakujte. Jinak obraťte se na správce systému.

- *Chyba: Zadaná cesta a název souboru jsou příliš dlouhé. Plně kvalifikovaný název souboru musí být méně než 260 znaků a název adresáře musí být méně než 248 znaků.*

    Zkraťte názvy složek a zkuste to znovu.
