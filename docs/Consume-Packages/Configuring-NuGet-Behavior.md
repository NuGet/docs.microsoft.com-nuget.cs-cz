---
title: Konfigurace chování NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet.Config soubory řídit chování NuGet globálně i na jednotlivých projektů a jsou upraveny pomocí příkazu config nuget.
keywords: NuGet konfigurační soubory, NuGet konfigurace, nastavení chování NuGet, nastavení NuGet, Nuget.Config, NuGetDefaults.Config, výchozí hodnoty
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a575868894d5ca9992b1c9984cf4920bd2858209
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="configuring-nuget-behavior"></a>Konfigurace chování NuGet

Chování NuGet doprovází Akumulovaná nastavení v jedné nebo více `NuGet.Config` soubory (XML), které může existovat projektu - uživatel- a úrovně platná pro celý počítač. Globální konfiguraci `NuGetDefaults.Config` soubor také konkrétně nakonfiguruje zdroje balíčků. Nastavení se vztahují na všechny příkazy vydané v rozhraní příkazového řádku, konzoly Správce balíčků a uživatelského rozhraní Správce balíčků.

## <a name="config-file-locations-and-uses"></a>Umístění konfiguračního souboru a používá

| Rozsah | Umístění souboru NuGet.Config | Popis |
| --- | --- | --- |
| Projekt | Aktuální složce (neboli složky projektu) nebo libovolné složky až kořenové jednotce.| Ve složce projektu nastavení platí pouze pro tento projekt. V nadřazené složky, které obsahují více projektů podsložky nastavení se vztahují na všechny projekty v těchto podsložky. |
| Uživatel | Windows: `%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux: `~/.nuget/NuGet/NuGet.Config` | Nastavení platí pro všechny operace, ale jsou přepsány jakékoli nastavení projektu. |
| Počítače | Windows: `%ProgramFiles(x86)%\NuGet\Config`<br/>Mac/Linux: `$XDG_DATA_HOME` (obvykle `~/.local/share`) | Nastavení platí pro všechny operace v počítači, ale jsou elementem podle všechna nastavení na úrovni uživatele nebo projektu. |

Poznámky pro starší verze balíčku nuget:
- NuGet 3.3 a dříve slouží `.nuget` složku pro nastavení celé řešení. Tento soubor není použit v NuGet 3.4 +.
- Pro NuGet 2.6 k 3.x, úrovni počítače konfiguračním souboru v systému Windows se nacházel v % ProgramData%\NuGet\Config [\\{IDE} [\\{Version} [\\{SKU}]]]\NuGet.Config, kde *{IDE}* může být  *Visual Studio*, *{Version}* verzi sady Visual Studio, jako byl *14.0*, a *{SKU}* je buď *komunity*, *Pro*, nebo *Enterprise*. Migrace nastavení na NuGet 4.0 +, jednoduše zkopírujte do konfiguračního souboru % ProgramFiles(x86) % \NuGet\Config. V systému Linux, byl tento předchozího umístění /etc/opt a v systému Mac, Library/Application Support.

## <a name="changing-config-settings"></a>Změna nastavení konfigurace

A `NuGet.Config` soubor je jednoduchý textový soubor XML obsahující dvojice klíč/hodnota, jak je popsáno v [nastavení konfigurace NuGet](../reference/nuget-config-file.md) tématu.

Nastavení se spravují pomocí rozhraní příkazového řádku NuGet [příkazu config](../tools/cli-ref-config.md):
- Ve výchozím nastavení provedení změn na úrovni uživatele konfiguračním souboru.
- Chcete-li změnit nastavení v jiném souboru, použijte `-configFile` přepínače. Soubory v tomto případě můžete použít libovolný název souboru.
- Klíče jsou vždy velká a malá písmena.
- Chcete-li změnit nastavení v souboru nastavení na úrovni počítače se vyžaduje zvýšení oprávnění.

> [!Warning]
> I když můžete upravit soubor v každém textovém editoru, NuGet (v3.4.3 a novější) bezobslužně ignoruje celý konfigurační soubor, pokud obsahuje poškozený obsah XML (Neshoda značek, neplatné znaky uvozovek atd.). To je důvod, proč je vhodnější ke správě nastavení pomocí `nuget config`.

### <a name="setting-a-value"></a>Nastavení hodnoty

Windows:

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\NuGet.Config
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
> V NuGet 3.4 a novější proměnné prostředí v jakákoli hodnota, můžete použít jako v `repositoryPath=%PACKAGEHOME%` (Windows) a `repositoryPath=%PACKAGEHOME` (Mac/Linux).

### <a name="removing-a-value"></a>Odebrání hodnotu

Odebrat hodnotu, zadejte klíč s prázdnou hodnotu.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Vytvoření nového souboru config

Zkopírujte šablony níže do nového souboru a pak použijte `nuget config -configFile <filename>` nastavit hodnoty:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Jak se používají nastavení

Více `NuGet.Config` soubory můžete ukládat nastavení v různých umístěních, tak, aby se vztahují na jeden projekt, skupinu projektů nebo všechny projekty. Toto nastavení se souhrnně platí pro všechny operace NuGet vyvolat z příkazového řádku nebo ze sady Visual Studio, s nastavením, které existují "nejbližší" do projektu nebo aktuální složce trvá prioritu.

Konkrétně NuGet načte nastavení z jiné konfigurační soubory v následujícím pořadí:

1. [NuGetDefaults.Config souboru](#nuget-defaults-file), který obsahuje nastavení týkající se pouze zdroje balíčků.
1. Soubor úrovni počítačů.
1. Soubor úrovni uživatele.
1. Zadaný soubor s `-configFile`.
1. Soubory, které jsou v každé složky v cestě z kořenového adresáře disku do aktuální složky (kde je volána nuget.exe nebo složku obsahující projekt Visual Studio). Například pokud je příkaz je vyvolána v c:\A\B\C, NuGet vyhledá a načte konfigurační soubory v c:\, pak c:\A, pak c:\A\B a nakonec c:\A\B\C.

Jako NuGet najde nastavení v těchto souborech, se používají takto:

1. U jedné položky elementů NuGet nahradit hodnotou dřív nalezený pro stejný klíč. To znamená, že nastavení, které jsou "nejbližší" do aktuální složky nebo projektu přepsat všechny další nalezeny dříve. Například `defaultPushSource` nastavení v `NuGetDefaults.Config` je přepsat, pokud existuje v jiné konfigurační soubor.

1. Pro elementy v kolekci (například `<packageSources>`), NuGet kombinuje hodnoty z všechny konfigurační soubory do jedné kolekce.

1. Když `<clear />` je k dispozici pro daný uzel NuGet ignoruje dříve definovaném konfigurační hodnoty pro tento uzel.

### <a name="settings-walkthrough"></a>Postup nastavení

Může se stát, že máte následující strukturu složek na dvě samostatné jednotky:

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

Budete mít čtyři `NuGet.Config` soubory v následujících umístěních s daný obsah. (Soubor úrovni počítače není zahrnutý v tomto příkladu, ale budou chovat podobně do souboru úrovni uživatele.)

Soubor A. individuální souborů, (`%appdata%\NuGet\NuGet.Config` v systému Windows, `~/.nuget/NuGet/NuGet.Config` na Mac/Linux):

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

File D. disk_drive_2/Project2/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

NuGet potom načte a aplikuje nastavení následujícím způsobem v závislosti na tom, kde je možné:

- **Volat z disk_drive_1 či uživatelů**: se používá pouze výchozí úložiště uvedené v souboru konfigurace na uživatelské úrovni (A), protože se jedná o jediný soubor na disk_drive_1 nalezen.

- **Volat z disk_drive_2 / nebo disk_drive_/tmp**: nejdřív načtení individuální souboru (A) a NuGet přejde do kořenového adresáře disk_drive_2 a najde soubor (B). NuGet rovněž vyhledává konfigurační soubor v TMP však nebyl nalezen jeden. V důsledku toho se používá výchozí úložiště na nuget.org, je povoleno obnovení balíčků a balíčky získat rozšířit disk_drive_2/tmp.

- **Volána z disk_drive_2/Project1 nebo disk_drive_2/Project1/zdroje**: nejdřív načtení individuální souboru (A) a potom NuGet načítání souboru (B) z kořenové složky disk_drive_2, za nímž následuje souboru (C). Nastavení v (C) přepíšou nastavení v (B) (A) a proto `repositoryPath` získat nainstalovanou balíčků je disk_drive_2/Project1/externí nebo balíčky místo *disk_drive_2/tmp*. Navíc vzhledem k tomu, že (C) vymaže `<packageSources>`, nuget.org již není k dispozici jako zdroj ponechat pouze `https://MyPrivateRepo/ES/nuget`.

- **Volána z disk_drive_2/projektu2 nebo disk_drive_2/projektu2/zdroje**: načtení individuální souboru (A) nejprve následuje soubor (B) a soubor (D). Protože `packageSources` není zaškrtnuto, obě `nuget.org` a `https://MyPrivateRepo/DQ/nuget` jsou k dispozici jako zdroje. Balíčky získat rozšířit disk_drive_2/tmp zadané v (B).

## <a name="nuget-defaults-file"></a>Výchozí nastavení souboru NuGet

`NuGetDefaults.Config` Soubor existuje, můžete určit zdroje balíčků, ze kterých jsou nainstalované a aktualizovat balíčky a řídit výchozí cíl pro publikování balíčků s `nuget push`. Protože správci můžou pohodlně (například pomocí zásad skupiny) nasadit konzistentní `NuGetDefaults.Config` soubory na vývojáře a sestavení počítače, můžete zajistit, že všichni uživatelé v organizaci používá správný balíček zdroje místo nuget.org.

> [!Important]
> `NuGetDefaults.Config` Souboru nikdy způsobí, že zdroj balíčku, který se odeberou z konfigurace NuGet pro vývojáře. To znamená, pokud vývojář již použit NuGet a proto má zdroj balíčku nuget.org registrován, nebude odebraný po vytvoření `NuGetDefaults.Config` souboru.
>
> Kromě toho, ani `NuGetDefaults.Config` ani jiným mechanismem v NuGet můžete zabránit přístupu do zdroje balíčků jako nuget.org. Pokud organizace chce blokovat takový přístup, použijte mnohem jiným způsobem, jako jsou brány firewall tak.

### <a name="nugetdefaultsconfig-location"></a>NuGetDefaults.Config umístění

Následující tabulka popisuje, kde `NuGetDefaults.Config` souboru by měly být uložené v závislosti na cílový operační systém:

| Platforma operačního systému  | NuGetDefaults.Config Location |
| --- | --- |
| Windows      | **Visual Studio 2017 nebo NuGet 4.x+:** % ProgramFiles (x86) %\NuGet\Config <br />**Visual Studio 2015 a starší nebo NuGet 3.x a starší:** %PROGRAMDATA%\NuGet |
| Mac/Linux    | XDG_DATA_HOME $ (obvykle ~/.local/share)|

### <a name="nugetdefaultsconfig-settings"></a>Nastavení NuGetDefaults.Config

- `packageSources`: Tato kolekce nemá stejný význam jako `packageSources` v regulárním konfigurační soubory a určí výchozí zdroje. NuGet používá zdroje v pořadí při instalaci nebo aktualizaci balíčků v projektech pomocí `packages.config` formátu správy. Pro projekty formátu PackageReference NuGet nejprve používá místní zdroje a pak zdroje v síťové sdílené složky a zdrojů HTTP, bez ohledu na pořadí v konfiguračních souborech. NuGet vždy ignoruje pořadí zdrojů s operací obnovení.

- `disabledPackageSources`: Tato kolekce také nemá stejný význam jako v `NuGet.Config` soubory, kde každý ovlivněných zdroj uvedené podle jeho název a hodnotu true nebo false, která určuje, zda je zakázána. To umožňuje zdroj název a adresu URL zůstat v `packageSources` bez nutnosti ho ve výchozím nastavení zapnuto. Jednotlivé vývojáři mohou pak znovu povolit zdroj nastavením hodnoty na zdroji na hodnotu false v jiných `NuGet.Config` soubory bez nutnosti znovu najít správnou adresu URL. To je užitečné k poskytování vývojářům úplný seznam adres URL vnitřní zdroj pro organizaci při povolování pouze jednotlivé team zdroje ve výchozím nastavení.

- `defaultPushSource`: Určuje výchozí cíl pro `nuget push` operace, přepsání předdefinovaných výchozí nuget.org. Správci mohou nasadit toto nastavení, aby se zabránilo publikování interní balíčky do veřejné nuget.org omylem odstraněný, jako vývojáři, konkrétně musí používat `nuget push -Source` publikovat do nuget.org.

### <a name="example-nugetdefaultsconfig-and-application"></a>Příklad NuGetDefaults.Config a aplikací

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
