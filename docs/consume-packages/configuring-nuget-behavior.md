---
title: Konfigurace chování nugetu
description: Soubor NuGet.Config soubory řízení chování Nugetu globálně i na základě jednotlivých projektů a jsou upraveny pomocí příkazu config nuget.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: c23b464ca39fd8d872f21846a7d6d34edf9dce93
ms.sourcegitcommit: 1bd72dca2f85b4267b9924236f1d23dd7b0ed733
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50088929"
---
# <a name="configuring-nuget-behavior"></a>Konfigurace chování Nugetu

Chování Nugetu doprovází nahromaděné nastavení v jedné nebo více `NuGet.Config` soubory (XML), které mohou existovat úrovni projektu –, uživatel- a celý počítač. Globální `NuGetDefaults.Config` soubor nastaví také konkrétně zdroje balíčků. Nastavení platí pro všechny příkazy vydané v rozhraní příkazového řádku, konzole Správce balíčků a uživatelské rozhraní Správce balíčků.

## <a name="config-file-locations-and-uses"></a>Umístění souboru konfigurace a použití

| Rozsah | Umístění souboru NuGet.Config | Popis |
| --- | --- | --- |
| Projekt | Aktuální složce (označuje se také jako složka projektu) nebo libovolnou složku do kořenové jednotky.| Ve složce projektu nastavení platí jenom pro daný projekt. V nadřazené složky, které obsahují více projektů podsložky nastavení platí pro všechny projekty v těchto podsložky. |
| Uživatel | Windows: `%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux: `~/.config/NuGet/NuGet.Config` nebo `~/.nuget/NuGet/NuGet.Config` (se liší podle operačního systému distribučního) | Nastavení platí pro všechny operace, ale jsou přepsány všechna nastavení na úrovni projektu. |
| Počítače | Windows: `%ProgramFiles(x86)%\NuGet\Config`<br/>Mac/Linux: `$XDG_DATA_HOME`. Pokud `$XDG_DATA_HOME` má hodnotu null nebo je prázdný, `~/.local/share` nebo `/usr/local/share` použije (se liší podle operačního systému distribučního)  | Nastavení platí pro všechny operace v počítači, ale jsou přepsány žádné nastavení na úrovni uživatele nebo projektu. |

Poznámky pro starší verze balíčku nuget:
- NuGet 3.3 a dříve použitých `.nuget` složku pro nastavení řešení. Tento soubor není používán ve Správci NuGet 3.4 +.
- NuGet 2.6 3.x, počítač úrovně konfiguračním souboru na Windows se nachází v % ProgramData%\NuGet\Config [\\{IDE} [\\{Version} [\\{SKU}]]]\NuGet.Config, kde *{IDE}* může být  *Visual Studio*, *{Version}* , jako je verze sady Visual Studio *14.0*, a *{SKU}* je buď *komunity*, *Pro*, nebo *Enterprise*. Migrace nastavení na NuGet 4.0 +, jednoduše zkopírujte konfigurační soubor do % ProgramFiles(x86) % \NuGet\Config. V Linuxu, byl tento předchozí umístění /etc/opt a na Macu, Library/Application Support.

## <a name="changing-config-settings"></a>Změna nastavení konfigurace

A `NuGet.Config` souboru je jednoduchý textový soubor XML obsahující dvojice klíč/hodnota, jak je popsáno v [nastavení konfigurace NuGet](../reference/nuget-config-file.md) tématu.

Nastavení se spravují pomocí rozhraní příkazového řádku NuGet [příkaz config](../tools/cli-ref-config.md):
- Ve výchozím nastavení jsou provedeny změny na úrovni uživatele konfiguračního souboru.
- Chcete-li změnit nastavení v jiném souboru, použijte `-configFile` přepnout. Soubory v tomto případě můžete použít libovolný název souboru.
- Klíče jsou vždy velká a malá písmena.
- Chcete-li změnit nastavení v souboru nastavení na úrovni počítače se vyžaduje zvýšení oprávnění.

> [!Warning]
> I když můžete upravit soubor v libovolném textovém editoru, NuGet (v3.4.3 a novější) tiše ignoruje celý konfigurační soubor, pokud obsahuje nesprávně vytvořeným kódem XML (Neshoda značek, uvozovky neplatný atd.). To je důvod, proč je vhodnější ke správě nastavení pomocí `nuget config`.

### <a name="setting-a-value"></a>Nastavení hodnoty

Windows:

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

Mac/Linux:

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> NuGet 3.4 a vyšší můžete použít proměnné prostředí v libovolnou hodnotu, jako v `repositoryPath=%PACKAGEHOME%` (Windows) a `repositoryPath=$PACKAGEHOME` (Mac/Linux).

### <a name="removing-a-value"></a>Odebrat hodnotu

Pokud chcete odebrat hodnotu, zadejte klíč s prázdnou hodnotu.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Vytvoření nového souboru config

Zkopírujte šablonu níže do nového souboru a pak použijte `nuget config -configFile <filename>` k nastavení hodnot:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Jak se používají nastavení

Více `NuGet.Config` soubory umožňují ukládat nastavení v různých umístěních, aby se vztahují na jednoho projektu, skupinu projektů nebo všechny projekty. Tato nastavení se souhrnně platí pro všechny operace NuGet vyvolat z příkazového řádku nebo z aplikace Visual Studio s nastavením, které existují "nejbližší" do projektu nebo aktuální složce trvá prioritu.

Konkrétně NuGet načte nastavení z jiné konfigurační soubory v následujícím pořadí:

1. [NuGetDefaults.Config souboru](#nuget-defaults-file), který obsahuje nastavení související jenom s zdroje balíčků.
1. Soubor úrovni počítače.
1. Uživatelské úrovni souboru.
1. Soubor určený parametrem `-configFile`.
1. Soubory nalezené v každé složky v cestě z kořenového adresáře disku do aktuální složky (Pokud je vyvolána nuget.exe nebo na složku obsahující projekt sady Visual Studio). Například, pokud příkaz je vyvolán v c:\A\B\C, NuGet vyhledá a načte konfigurační soubory v c:\, pak c:\A pak c:\A\B a nakonec c:\A\B\C.

Jak NuGet najde nastavení v těchto souborech, použijí se následujícím způsobem:

1. Pro prvky jedné položky NuGet nahradit libovolnou dříve najít hodnotu pro stejný klíč. To znamená, že nastavení, které jsou "co nejblíž koncovým" aktuální složku nebo projekt přepsat všechny ostatní nalezen dříve. Například `defaultPushSource` nastavení `NuGetDefaults.Config` je přepsána, pokud existuje v jiném konfiguračním souboru.

1. Kolekce elementů (například `<packageSources>`), NuGet kombinuje hodnoty z všechny konfigurační soubory do jedné kolekce.

1. Když `<clear />` je k dispozici pro daný uzel NuGet ignoruje dříve definovaným hodnotám konfigurace pro tento uzel.

### <a name="settings-walkthrough"></a>Názorný postup nastavení

Řekněme, že mají následující strukturu složek na dvě samostatné jednotky:

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

Pak máte čtyři `NuGet.Config` soubory v následujících umístěních se daný obsah. (Soubor úrovni počítače není zahrnuta v tomto příkladu, ale by se chovají podobně uživatelské úrovni souboru.)

Soubor individuální A. (`%appdata%\NuGet\NuGet.Config` na Windows, `~/.config/NuGet/NuGet.Config` na Mac/Linux):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

Soubor B. disk_drive_2/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="disk_drive_2/tmp" />
    </config>
    <packageRestore>
        <add key="enabled" value="True" />
    </packageRestore>
</configuration>
```

Soubor C. disk_drive_2/Project1/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="External/Packages" />
        <add key="defaultPushSource" value="https://MyPrivateRepo/ES/api/v2/package" />
    </config>
    <packageSources>
        <clear /> <!-- ensure only the sources defined below are used -->
        <add key="MyPrivateRepo - ES" value="https://MyPrivateRepo/ES/nuget" />
    </packageSources>
</configuration>
```

Disk_drive_2/Project2/NuGet.Config D. souboru:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

NuGet pak načte a použije nastavení následujícím způsobem, v závislosti na tom, kde je vyvolána:

- **Vyvolat z disk_drive_1/uživatele v**: se používá pouze výchozí úložiště uvedené v souboru konfigurace na úrovni uživatele (A), protože se jedná o jediný soubor na disk_drive_1.

- **Vyvolat z disk_drive_2 / nebo disk_drive_/tmp**: individuální souboru (A) je načten jako první, potom NuGet přejde do kořenového adresáře disk_drive_2 a najde soubor (B). NuGet také hledá v konfiguračním souboru v TMP, ale nebyl nalezen jeden. V důsledku toho se používá výchozí úložiště na nuget.org, obnovení balíčku je povolená a balíčky získat rozbalení v disk_drive_2/tmp.

- **Vyvolání z disk_drive_2/Project1 nebo disk_drive_2/Project1/zdroje**: nejprve načtení souboru individuální (A) a pak NuGet načtení souboru (B) z kořenového adresáře disk_drive_2, za nímž následuje souboru (C). Nastavení v (C) mají přednost před akcemi v (B) (A) a proto `repositoryPath` kde instalovat balíčky je disk_drive_2/Project1/externí/balíčky místo *disk_drive_2/tmp*. Navíc protože (C) vymaže `<packageSources>`, nuget.org již není k dispozici jako zdroj byste museli opustit pouze `https://MyPrivateRepo/ES/nuget`.

- **Vyvolání z disk_drive_2 / "project2" nebo disk_drive_2 / "project2" / zdroje**: načtení souboru individuální (A) nejprve následovaný soubor (B) a soubor (D). Protože `packageSources` není zaškrtnuto, obě `nuget.org` a `https://MyPrivateRepo/DQ/nuget` jsou k dispozici jako zdroje. Získejte balíčky rozbalení v disk_drive_2/tmp, jak je uvedeno v (B).

## <a name="nuget-defaults-file"></a>Soubor výchozích hodnot NuGet

`NuGetDefaults.Config` Soubor existuje, můžete určit zdroje balíčků, ze kterých jsou nainstalované a aktualizovat balíčky a řídit výchozí cíl pro publikování balíčky s `nuget push`. Protože správci můžou jednoduše (například pomocí zásad skupiny) nasadit konzistentní `NuGetDefaults.Config` soubory na vývojáře a počítače sestavení, můžete zajistit, že všichni uživatelé v organizaci používá správný balíček zdroje místo nuget.org.

> [!Important]
> `NuGetDefaults.Config` Souboru nikdy způsobí, že zdroj balíčku, který chcete odebrat z konfigurace NuGet pro vývojáře. To znamená, že pokud se už používá NuGet vývojář a proto má zdroj balíčku nuget.org zaregistrovali, se neodstraní po vytvoření `NuGetDefaults.Config` souboru.
>
> Kromě toho, ani `NuGetDefaults.Config` ani jiný mechanismus ve Správci NuGet můžete zabránit přístupu k balíčku zdrojů, jako je nuget.org. Pokud organizace si přeje blokovat takový přístup, musí k tomu používat jiným způsobem, jako jsou brány firewall.

### <a name="nugetdefaultsconfig-location"></a>NuGetDefaults.Config umístění

Následující tabulka popisuje, kde `NuGetDefaults.Config` souboru by měla být uložena v závislosti na použitý operační systém:

| Platforma operačního systému  | NuGetDefaults.Config umístění |
| --- | --- |
| Windows      | **Visual Studio 2017 nebo NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 a starší nebo NuGet 3.x a dříve:** `%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME` (obvykle `~/.local/share` nebo `/usr/local/share`, v závislosti na operačním systémem distribuce)|

### <a name="nugetdefaultsconfig-settings"></a>Nastavení NuGetDefaults.Config

- `packageSources`: Tato kolekce nemá stejný význam jako `packageSources` ve standardní konfigurační soubory a určí výchozí zdroje. NuGet používá zdroje v pořadí při instalaci nebo aktualizaci balíčky v projektech pomocí `packages.config` formátu správy. Pro projekty ve formátu PackageReference NuGet nejprve používá místní zdroje a pak zdrojů na sdílené síťové složky a zdrojů HTTP, bez ohledu na pořadí, v konfiguračních souborech. NuGet vždy ignoruje pořadí zdrojů s operacemi obnovení.

- `disabledPackageSources`: Tato kolekce má také stejný význam jako v `NuGet.Config` soubory, kde každý ovlivněné zdroj uvedené podle jeho název a hodnotu true nebo false určující, zda je zakázána. To umožňuje název zdroje a adresa URL tak si zachováte `packageSources` bez nutnosti ho ve výchozím nastavení zapnutá. Jednotliví vývojáři můžete potom znovu povolit zdroj podle zdroje na hodnotu nastavíte na hodnotu false v ostatních `NuGet.Config` soubory, aniž byste museli znovu najít správnou adresu URL. To je užitečné k poskytování vývojářům úplný seznam adres URL vnitřního zdroje pro organizaci při povolování pouze zdroj jednotlivý tým ve výchozím nastavení.

- `defaultPushSource`: Určuje výchozí cíl pro `nuget push` operace, přepíšete integrovanou výchozí nuget.org. Správci můžou nasadit tohoto nastavení můžete zabránit publikování interní balíčků na nuget.org veřejné omylem, jak vývojáři konkrétně muset použít `nuget push -Source` publikovat na nuget.org.

### <a name="example-nugetdefaultsconfig-and-application"></a>Příklad NuGetDefaults.Config a aplikace

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- defaultPushSource key works like the 'defaultPushSource' key of NuGet.Config files. -->
    <!-- This can be used by administrators to prevent accidental publishing of packages to nuget.org. -->
    <config>
        <add key="defaultPushSource" value="https://contoso.com/packages/" />
    </config>

    <!-- Default Package Sources; works like the 'packageSources' section of NuGet.Config files. -->
    <!-- This collection cannot be deleted or modified but can be disabled/enabled by users. -->
    <packageSources>
        <add key="Contoso Package Source" value="https://contoso.com/packages/" />
        <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    </packageSources>

    <!-- Default Package Sources that are disabled by default. -->
    <!-- Works like the 'disabledPackageSources' section of NuGet.Config files. -->
    <!-- Sources cannot be modified or deleted either but can be enabled/disabled by users. -->
    <disabledPackageSources>
        <add key="nuget.org" value="true" />
    </disabledPackageSources>
</configuration>
```
