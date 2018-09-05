---
title: Správa globálních balíčků, mezipaměť, dočasné složky ve Správci NuGet
description: Jak spravovat globální balíčku Instalační složka mezipaměti balíčku a dočasné složky, které existují na počítači, které se použijí při instalaci, obnovení a aktualizace balíčků.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: c547ae1d46079d040d7c3aa4c7678e70cd199dce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548010"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Správa globálních balíčků, mezipaměť a dočasné složky

Pokaždé, když se nainstalovat, aktualizovat nebo obnovit balíček NuGet spravuje balíčky a informace o balíčku v mimo strukturu projektu několik složek:

| Název | Popis a umístění (na jednoho uživatele)|
| --- | --- |
| globální&#8209;balíčky | *Global-packages* kde NuGet nainstaluje všechny staženého balíčku je složka. Každý balíček je úplně rozbalen do podsložky, která odpovídá identifikátor balíčku a číslo verze. Projekty pomocí PackageReference formátu vždy balíčky pro použití přímo z této složky. Při použití `packages.config`, balíčky se nainstalují do *global-packages* složku, pak zkopíruje do projektu `packages` složky.<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>Přepsat pomocí proměnné prostředí NUGET_PACKAGES `globalPackagesFolder` nebo `repositoryPath` [nastavení konfigurace](../reference/nuget-config-file.md#config-section) (při použití PackageReference a `packages.config`v uvedeném pořadí), nebo `RestorePackagesPath` MSBuild vlastnosti (pouze nástroj MSBuild). Proměnná prostředí má přednost před nastavením konfigurace.</li></ul> |
| http&#8209;cache | Balíček správce sady Visual Studio (NuGet 3.x+) a `dotnet` nástroj úložiště kopie v mezipaměti stažených balíčků (Uložit jako `.dat` soubory) uspořádaných do podsložky pro jednotlivé zdroje balíčku. Balíčky nejsou rozbalen a mezipaměti má čas vypršení platnosti 30 minut.<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>Přepište NUGET_HTTP_CACHE_PATH proměnné prostředí.</li></ul> |
| temp | Složka, ve kterém NuGet ukládá dočasné soubory během jeho různé operace.<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |
| moduly plug-in mezipaměti **4.8 +** | Složky, kde NuGet uchovává výsledky z deklarací identity požadavek operation.<br/><ul><li>Windows: `%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/plugins-cache`</li><li>Přepište NUGET_PLUGINS_CACHE_PATH proměnné prostředí.</li></ul> |

> [!Note]
> NuGet 3.5 a starších používá *mezipaměť balíčků* místo *http-cache*, který se nachází v `%localappdata%\NuGet\Cache`.

Mezipaměť a *global-packages* složek, NuGet obecně se vyhnete stahovali balíčky, které již existují na počítači, vylepšení výkonu instalovat, aktualizovat a operace obnovení. Při použití PackageReference, *global-packages* složku také zabraňuje uchování stáhnout balíčky uvnitř složky projektu, kde se může nechtěně přidat do správy zdrojového kódu a snižuje celkový dopad NuGet na počítači úložiště.

Když se zobrazí výzva k načtení balíčku, nejprve hledá NuGet v *global-packages* složky. Pokud není přesné verze balíčku, NuGet kontroluje všechny zdroje balíčků jiným protokolem než HTTP. Pokud balíček není stále nalezen, NuGet hledá v balíčku *http-cache* neurčíte `--no-cache` s `dotnet.exe` příkazy nebo `-NoCache` s `nuget.exe` příkazy. Pokud balíček není v mezipaměti, nebo do mezipaměti se nepoužívá, NuGet pak načte balíček přes protokol HTTP.

Další informace najdete v tématu [co se stane, když je nainstalován balíček](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).

## <a name="viewing-folder-locations"></a>Zobrazení umístění složek

Zobrazí se umístění s využitím [příkaz nuget locals](../tools/cli-ref-locals.md):

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

Příklad typického výstupu (Windows; aktuální uživatelské jméno je "uživatel1"):

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

(`package-cache` používá NuGet 2.x a zobrazí se u NuGet 3.5 a starší.)

Umístění složky s využitím můžete zobrazit také [příkaz dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals):

```cli
dotnet nuget locals all --list
```

Příklad typického výstupu (Mac/Linux; aktuální uživatelské jméno je "uživatel1"):

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

Chcete-li zobrazit umístění jednotlivých složek, použijte `http-cache`, `global-packages`, `temp`, nebo `plugins-cache` místo `all`.

## <a name="clearing-local-folders"></a>Vymazává se místní složky

Pokud docházet k problémům při instalaci balíčku nebo jinak chcete zajistit, že instalujete balíčky ze vzdáleného galerii, použijte `locals --clear` možnost (dotnet.exe) nebo `locals -clear` (nuget.exe) určující složku, kterou chcete vymazat, nebo `all` do Vymažte všechny složky:

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

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

Všechny balíčky, které používají projekty, které jsou právě otevřeny v sadě Visual Studio se vymazat z *global-packages* složky.

V sadě Visual Studio 2017, použijte **nástroje > Správce balíčků NuGet > Nastavení správce balíčků** nabídce příkaz a pak vyberte **vymazat všechny mezipaměti NuGet**. Správa mezipaměti není v současné době dostupná přes konzolu Správce balíčků. V sadě Visual Studio 2015 pomocí příkazů rozhraní příkazového řádku.

![Příkaz NuGet možnost pro vymazání mezipaměti](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Řešení potíží s chybami

Těmto chybám může dojít při použití `nuget locals` nebo `dotnet nuget locals`:

- *Chyba: Proces nemá přístup k souboru <package> protože ho používá jiný proces* nebo *vymazat místní prostředky se nezdařilo: nelze odstranit jeden nebo více souborů*

    Jeden nebo více souborů ve složce se používají v jiném procesu; otevřít, který odkazuje na balíčky v projektu sady Visual Studio je třeba *global-packages* složky. Zavřít tyto procesy a zkuste to znovu.

- *Chyba: Přístup k cestě <path> odepřen* nebo *adresář není prázdný*

    Nemáte oprávnění k odstranění souborů v mezipaměti. Změnit oprávnění, pokud je to možné a zkuste to znovu. Jinak obraťte se na správce systému.

- *Chyba: Zadaná cesta, název souboru nebo obojí jsou příliš dlouhé. Plně kvalifikovaný název musí být kratší než 260 znaků a název adresáře musí být kratší než 248 znaků.*

    Zkraťte název složky a zkuste to znovu.
