---
title: Správa globálních balíčků, mezipaměti, dočasných složek v NuGetu
description: Jak spravovat instalační složku globálního balíčku, mezipaměť balíčků a dočasné složky, které existují na počítači, které se používají při instalaci, obnovení a aktualizaci balíčků.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e2672aa0bf57242526364639f0df74f9d1adb934
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428966"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Správa globálních balíčků, mezipaměti a dočasných složek

Kdykoli nainstalujete, aktualizujete nebo obnovíte balíček, aplikace NuGet spravuje balíčky a informace o balíčcích v několika složkách mimo vaši strukturu projektu:

| Název | Popis a umístění (na uživatele)|
| --- | --- |
| globální&#8209;balíčky | Složka *Global-Packages* je místo, kde NuGet nainstaluje libovolný stažený balíček. Každý balíček je plně rozbalen do podsložky, která odpovídá identifikátoru a číslu verze balíčku. Projekty, které používají formát [PackageReference](package-references-in-project-files.md) , vždy používají balíčky přímo z této složky. Při použití [souboru Packages. config](../reference/packages-config.md)se balíčky nainstalují do složky *Global-Packages* a pak se zkopírují do složky `packages` projektu.<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>Popište pomocí proměnné prostředí NUGET_PACKAGES, [nastavení konfigurace](../reference/nuget-config-file.md#config-section) `globalPackagesFolder` nebo `repositoryPath` (při použití PackageReference a `packages.config`) nebo vlastnosti `RestorePackagesPath` MSBuild (jenom MSBuild). Proměnná prostředí má přednost před nastavením konfigurace.</li></ul> |
| http&#8209;cache | Správce balíčků sady Visual Studio (NuGet 3. x +) a nástroj `dotnet` ukládá kopie stažených balíčků v této mezipaměti (uložené jako `.dat` soubory) uspořádané do podsložek pro každý zdroj balíčku. Balíčky nejsou rozbalené a mezipaměť má čas vypršení platnosti 30 minut.<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>Přepsat pomocí proměnné prostředí NUGET_HTTP_CACHE_PATH.</li></ul> |
| temp | Složka, ve které NuGet ukládá dočasné soubory během různých operací.<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |
| moduly plug-in – mezipaměť **4,8 +** | Složka, ve které NuGet ukládá výsledky z požadavku na Operations identity<br/><ul><li>Windows: `%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/plugins-cache`</li><li>Přepsat pomocí proměnné prostředí NUGET_PLUGINS_CACHE_PATH.</li></ul> |

> [!Note]
> NuGet 3,5 a starší používá místo *mezipaměti HTTP-* cache, která je umístěná v `%localappdata%\NuGet\Cache`, *mezipaměť balíčků* .

Pomocí složek cache a *Global-Packages* NuGet se obecně vyhne stahování balíčků, které již v počítači existují, což zlepšuje výkon operací instalace, aktualizace a obnovení. Při použití PackageReference se složka *Global-Packages* také vyhne zachovávání stažených balíčků ve složkách projektu, kde by mohly být neúmyslně přidány do správy zdrojových kódů, a snižuje celkový dopad na úložiště počítače.

Když se zobrazí výzva k načtení balíčku, NuGet nejprve vyhledá složku *Global-Packages* . Pokud není k dispozici přesná verze balíčku, vyhledá NuGet všechny zdroje balíčků bez HTTP. Pokud se balíček pořád nenašel, NuGet vyhledá balíček v *mezipaměti HTTP-cache* , pokud neurčíte `--no-cache` s příkazy `dotnet.exe` nebo `-NoCache` s `nuget.exe` příkazy. Pokud balíček není v mezipaměti, nebo se mezipaměť nepoužívá, NuGet ho načte pomocí protokolu HTTP.

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

(`package-cache` se používá v NuGet 2. x a zobrazí se s NuGet 3,5 a starším.)

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

Chcete-li zobrazit umístění jedné složky, použijte `http-cache`, `global-packages`, `temp`nebo `plugins-cache` namísto `all`.

## <a name="clearing-local-folders"></a>Mazání místních složek

Pokud narazíte na problémy s instalací balíčku nebo pokud chcete, aby se balíčky instalovaly ze vzdálené galerie, použijte možnost `locals --clear` (dotnet. exe) nebo `locals -clear` (NuGet. exe), zadejte složku, která se má vymazat, nebo `all` vymažte všechny složky:

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

Při použití `nuget locals` nebo `dotnet nuget locals`může dojít k následujícím chybám:

- *Chyba: proces nemůže získat přístup k souboru, <package> protože ho používá jiný proces* nebo *se nepovedlo vymazat místní prostředky: nepovedlo se odstranit jeden nebo víc souborů.*

    Jeden nebo více souborů ve složce používá jiný proces. například projekt sady Visual Studio je otevřen, který odkazuje na balíčky ve složce *Global-Packages* . Zavřete tyto procesy a zkuste to znovu.

- *Chyba: přístup k cestě <path> byl odepřen* nebo *adresář není prázdný* .

    Nemáte oprávnění k odstranění souborů v mezipaměti. Pokud je to možné, změňte oprávnění složky a zkuste to znovu. V opačném případě se obraťte na správce systému.

- *Chyba: Zadaná cesta, název souboru nebo obojí jsou příliš dlouhé. Plně kvalifikovaný název souboru musí být kratší než 260 znaků a název adresáře musí být kratší než 248 znaků.*

    Zkraťte název složky a zkuste to znovu.
