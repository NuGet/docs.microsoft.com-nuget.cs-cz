---
title: Správa globálních balíčků, mezipaměti, dočasných složek v NuGetu
description: Jak spravovat instalační složku globálního balíčku, mezipaměť balíčků a dočasné složky, které existují na počítači, které se používají při instalaci, obnovení a aktualizaci balíčků.
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e5585267d4ce2563d77ff30ec5c31e196d98686a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774795"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Správa globálních balíčků, mezipaměti a dočasných složek

Kdykoli nainstalujete, aktualizujete nebo obnovíte balíček, aplikace NuGet spravuje balíčky a informace o balíčcích v několika složkách mimo vaši strukturu projektu:

| Name | Popis a umístění (na uživatele)|
| --- | --- |
| balíčky globálních&#8209; | Složka *Global-Packages* je místo, kde NuGet nainstaluje libovolný stažený balíček. Každý balíček je plně rozbalen do podsložky, která odpovídá identifikátoru a číslu verze balíčku. Projekty, které používají formát [PackageReference](package-references-in-project-files.md) , vždy používají balíčky přímo z této složky. Při použití [packages.config](../reference/packages-config.md)balíčky se nainstalují do složky *Global-Packages* a pak se zkopírují do složky projektu `packages` .<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>Popište pomocí proměnné prostředí NUGET_PACKAGES, `globalPackagesFolder` `repositoryPath` [nastavení konfigurace](../reference/nuget-config-file.md#config-section) nebo (při použití PackageReference a v `packages.config` uvedeném pořadí) nebo `RestorePackagesPath` vlastnosti MSBuild (jenom MSBuild). Proměnná prostředí má přednost před nastavením konfigurace.</li></ul> |
| mezipaměť&#8209;http | Správce balíčků sady Visual Studio (NuGet 3. x +) a `dotnet` Nástroj ukládá kopie stažených balíčků v této mezipaměti (uložené jako `.dat` soubory), které jsou uspořádány do podsložek pro každý zdroj balíčku. Balíčky nejsou rozbalené a mezipaměť má čas vypršení platnosti 30 minut.<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>Přepsat pomocí proměnné prostředí NUGET_HTTP_CACHE_PATH.</li></ul> |
| temp | Složka, ve které NuGet ukládá dočasné soubory během různých operací.<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |
| moduly plug-in – mezipaměť **4,8 +** | Složka, ve které NuGet ukládá výsledky z požadavku na Operations identity<br/><ul><li>Windows: `%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/plugins-cache`</li><li>Přepsat pomocí proměnné prostředí NUGET_PLUGINS_CACHE_PATH.</li></ul> |

> [!Note]
> NuGet 3,5 a starší používá *mezipaměť balíčků* místo *HTTP-cache*, která je umístěna v `%localappdata%\NuGet\Cache` .

Pomocí složek cache a *Global-Packages* NuGet se obecně vyhne stahování balíčků, které již v počítači existují, což zlepšuje výkon operací instalace, aktualizace a obnovení. Při použití PackageReference se složka *Global-Packages* také vyhne zachovávání stažených balíčků ve složkách projektu, kde by mohly být neúmyslně přidány do správy zdrojových kódů, a snižuje celkový dopad na úložiště počítače.

Když se zobrazí výzva k načtení balíčku, NuGet nejprve vyhledá složku *Global-Packages* . Pokud není k dispozici přesná verze balíčku, vyhledá NuGet všechny zdroje balíčků bez HTTP. Pokud se balíček ještě nenašel, NuGet vyhledá balíček v *mezipaměti HTTP-cache* , pokud nezadáte `--no-cache` `dotnet.exe` příkazy s příkazy nebo `-NoCache` s `nuget.exe` příkazy. Pokud balíček není v mezipaměti, nebo se mezipaměť nepoužívá, NuGet ho načte pomocí protokolu HTTP.

Další informace najdete v tématu [co se stane, když se balíček nainstaluje?](../concepts/package-installation-process.md).

## <a name="viewing-folder-locations"></a>Zobrazení umístění složek

Umístění můžete zobrazit pomocí [příkazu NuGet Locals](../reference/cli-reference/cli-ref-locals.md):

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

Typický výstup (Windows; "Uživatel1" je aktuální uživatelské jméno:

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

( `package-cache` používá se v NuGet 2. x a zobrazí se nuget 3,5 a starším.)

Umístění složek můžete zobrazit také pomocí [příkazu dotnet NuGet Locals](/dotnet/core/tools/dotnet-nuget-locals):

```dotnetcli
dotnet nuget locals all --list
```

Typický výstup (Mac/Linux; "Uživatel1" je aktuální uživatelské jméno:

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

Chcete-li zobrazit umístění jedné složky, použijte `http-cache` ,, `global-packages` `temp` nebo `plugins-cache` místo `all` .

## <a name="clearing-local-folders"></a>Mazání místních složek

Pokud narazíte na problémy s instalací balíčku nebo pokud chcete, aby se balíčky instalovaly ze vzdálené galerie, použijte `locals --clear` možnost (dotnet.exe) nebo `locals -clear` (nuget.exe), zadejte složku, která se má vymazat, nebo `all` zrušte zaškrtnutí všech složek:

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

Všechny balíčky používané projekty, které jsou aktuálně otevřeny v aplikaci Visual Studio, nejsou vymazány ze složky *Global-Packages* .

V aplikaci Visual Studio 2017 použijte **Správce balíčků NuGet nástroje > > příkaz Správce balíčků** a pak vyberte **Vymazat všechny mezipaměti NuGet**. Správa mezipaměti není v současnosti k dispozici prostřednictvím konzoly Správce balíčků. V aplikaci Visual Studio 2015 použijte místo toho příkazy rozhraní příkazového řádku.

![Příkaz NuGet pro mazání mezipamětí](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Řešení chyb

Při použití nebo se můžou objevit tyto `nuget locals` chyby `dotnet nuget locals` :

- *Chyba: proces nemůže získat přístup k souboru, <package> protože ho používá jiný proces nebo došlo k chybě* při *mazání místních prostředků: nepovedlo se odstranit jeden nebo víc souborů.*

    Jeden nebo více souborů ve složce používá jiný proces. například projekt sady Visual Studio je otevřen, který odkazuje na balíčky ve složce *Global-Packages* . Zavřete tyto procesy a zkuste to znovu.

- *Chyba: přístup k cestě byl <path> odepřen* nebo *adresář není prázdný* .

    Nemáte oprávnění k odstranění souborů v mezipaměti. Pokud je to možné, změňte oprávnění složky a zkuste to znovu. V opačném případě se obraťte na správce systému.

- *Chyba: Zadaná cesta, název souboru nebo obojí jsou příliš dlouhé. Plně kvalifikovaný název souboru musí být kratší než 260 znaků a název adresáře musí být kratší než 248 znaků.*

    Zkraťte název složky a zkuste to znovu.
