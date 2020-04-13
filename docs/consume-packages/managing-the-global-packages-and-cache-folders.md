---
title: Jak spravovat globální balíčky, cache, dočasné složky v NuGet
description: Jak spravovat globální instalační složku balíčku, mezipaměť balíčků a dočasné složky, které existují v počítači a které se používají při instalaci, obnovení a aktualizaci balíčků.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e2672aa0bf57242526364639f0df74f9d1adb934
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428966"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Správa globálních balíčků, mezipaměti a dočasných složek

Kdykoli nainstalujete, aktualizujete nebo obnovíte balíček, nuget spravuje balíčky a informace o balíčku v několika složkách mimo strukturu projektu:

| Name (Název) | Popis a umístění (na uživatele)|
| --- | --- |
| globální&#8209;balíčky | Složka *globální balíčky* je místo, kde NuGet nainstaluje všechny stažené balíček. Každý balíček je plně rozbalen do podsložky, která odpovídá identifikátoru balíčku a číslo verze. Projekty používající formát [PackageReference](package-references-in-project-files.md) vždy používají balíčky přímo z této složky. Při použití [souboru packages.config](../reference/packages-config.md)jsou balíčky nainstalovány do složky *globálních balíčků* a poté zkopírovány do `packages` složky projektu.<br/><ul><li>Windows:`%userprofile%\.nuget\packages`</li><li>Mac/Linux:`~/.nuget/packages`</li><li>Přepsat `globalPackagesFolder` pomocí proměnné NUGET_PACKAGES prostředí, `repositoryPath` nastavení nebo [konfigurace](../reference/nuget-config-file.md#config-section) (při použití PackageReference a `packages.config`, příslušně) nebo `RestorePackagesPath` MSBuild vlastnost (Pouze MSBuild). Proměnná prostředí má přednost před nastavením konfigurace.</li></ul> |
| http&#8209;cache | Visual Studio Package Manager (NuGet 3.x+) a `dotnet` nástroj ukládat kopie stažených balíčků v této mezipaměti (uložené jako `.dat` soubory), uspořádané do podsložek pro každý zdroj balíčku. Balíčky nejsou rozbaleny a mezipaměť má dobu vypršení platnosti 30 minut.<br/><ul><li>Windows:`%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux:`~/.local/share/NuGet/v3-cache`</li><li>Přepsat pomocí proměnné prostředí NUGET_HTTP_CACHE_PATH.</li></ul> |
| Temp | Složka, kde NuGet ukládá dočasné soubory během různých operací.<br/><li>Windows:`%temp%\NuGetScratch`</li><li>Mac/Linux:`/tmp/NuGetScratch`</li></ul> |
| pluginy-cache **4,8+** | Složka, kde NuGet ukládá výsledky z požadavku deklarace identity operace.<br/><ul><li>Windows:`%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux:`~/.local/share/NuGet/plugins-cache`</li><li>Přepsat pomocí proměnné NUGET_PLUGINS_CACHE_PATH prostředí.</li></ul> |

> [!Note]
> NuGet 3.5 a starší používá *balíčky cache* namísto *http-cache*, který je umístěn v `%localappdata%\NuGet\Cache`.

Pomocí mezipaměti a *globální balíčky* složky NuGet obecně vyhýbá stahování balíčků, které již existují v počítači, zlepšení výkonu instalace, aktualizace a obnovení operací. Při použití PackageReference, *globální balíčky* složky také zabraňuje udržování stažené balíčky uvnitř složky projektu, kde mohou být neúmyslně přidány do správy zdrojového kódu a snižuje Celkový dopad NuGet na úložiště počítače.

Když budete vyzváni k načtení balíčku, NuGet nejprve vyhledá ve složce *globální balíčky.* Pokud přesná verze balíčku není k dispozici, pak NuGet zkontroluje všechny zdroje balíčku bez HTTP. Pokud balíček stále nebyl nalezen, NuGet hledá balíček v `--no-cache` *http-cache,* `nuget.exe` pokud zadáte pomocí `dotnet.exe` příkazů nebo `-NoCache` s příkazy. Pokud balíček není v mezipaměti nebo mezipaměti není použit, NuGet pak načte balíček přes HTTP .

Další informace naleznete v [tématu Co se stane, když je balíček nainstalován?](../concepts/package-installation-process.md).

## <a name="viewing-folder-locations"></a>Zobrazení umístění složek

Umístění můžete zobrazit pomocí [příkazu nuget locals](../reference/cli-reference/cli-ref-locals.md):

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

Typický výstup (Windows; "user1" je aktuální uživatelské jméno):

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

(`package-cache` se používá v NuGet 2.x a zobrazí se s NuGet 3.5 a starší.)

Umístění složek můžete také zobrazit pomocí [příkazu dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals):

```dotnetcli
dotnet nuget locals all --list
```

Typický výstup (Mac/Linux; "user1" je aktuální uživatelské jméno):

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

Chcete-li zobrazit umístění jedné `http-cache`složky, `plugins-cache` použijte `all`místo aplikace použití `global-packages`, `temp`, nebo .

## <a name="clearing-local-folders"></a>Vymazání místních složek

Pokud narazíte na problémy s instalací balíčku nebo chcete jinak zajistit, `locals --clear` že instalujete balíčky ze vzdálené galerie, použijte možnost (dotnet.exe) nebo `locals -clear` (nuget.exe) a určete složku, kterou chcete vymazat, nebo `all` vymazat všechny složky:

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

Všechny balíčky používané projekty, které jsou aktuálně otevřené v sadě Visual Studio nejsou vymazány ze složky *globální balíčky.*

Počínaje Visual Studio 2017, použijte **nástroje > NuGet Správce balíčků > nastavení správce balíčků,** pak vyberte **Vymazat všechny NuGet Cache (y)**. Správa mezipaměti není v současné době k dispozici prostřednictvím konzoly Správce balíčků. V sadě Visual Studio 2015 použijte příkazy příkazového příkazu.

![Příkaz možnosti NuGet pro vymazání mezipamětí](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Řešení chyb

Při použití `nuget locals` nebo `dotnet nuget locals`:

- *Chyba: Proces nemá přístup <package> k souboru, protože je používán jiným procesem* nebo *vymazáním místních prostředků se nezdařilo: Nelze odstranit jeden nebo více souborů.*

    Jeden nebo více souborů ve složce jsou používány jiným procesem; Například je otevřený projekt sady Visual Studio, který odkazuje na balíčky ve složce *globální balíčky.* Zavřete tyto procesy a akci opakujte.

- *Chyba: Přístup k <path> cestě je odepřen* nebo *adresář není prázdný.*

    Nemáte oprávnění k odstranění souborů v mezipaměti. Pokud je to možné, změňte oprávnění ke složce a akci opakujte. V opačném případě se obraťte na správce systému.

- *Chyba: Zadaná cesta, název souboru nebo obojí jsou příliš dlouhé. Úplný název souboru musí být menší než 260 znaků a název adresáře musí být menší než 248 znaků.*

    Zkraťte názvy složek a akci opakujte.
