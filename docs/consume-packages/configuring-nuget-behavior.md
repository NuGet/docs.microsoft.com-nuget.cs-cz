---
title: Běžné konfigurace NuGetu
description: NuGet.Config soubory řídit NuGet chování globálně i na základě projektu a jsou upraveny pomocí nuget config příkazu.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 89127203df0aa1eb24f36b8ec64c5bb4a4d59319
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428910"
---
# <a name="common-nuget-configurations"></a>Běžné konfigurace NuGetu

Chování nugetu je řízeno nahromaděnými nastaveními v jednom nebo více `NuGet.Config` (XML) souborech, které mohou existovat na úrovni celého projektu, uživatele a počítače. Globální `NuGetDefaults.Config` soubor také konkrétně konfiguruje zdroje balíčků. Nastavení platí pro všechny příkazy vydané v příkazech příkazu příkazu cli, konzoly správce balíčků a ui Správce balíčků.

## <a name="config-file-locations-and-uses"></a>Umístění a použití konfiguračních souborů

| Rozsah | Umístění souboru NuGet.Config | Popis |
| --- | --- | --- |
| Řešení | Aktuální složka (aka řešení složky) nebo libovolné složky až do kořenového adresáře jednotky.| Ve složce řešení platí nastavení pro všechny projekty v podsložkách. Všimněte si, že pokud je konfigurační soubor umístěn do složky projektu, nemá na tento projekt žádný vliv. |
| Uživatel | Windows:`%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux: `~/.config/NuGet/NuGet.Config` `~/.nuget/NuGet/NuGet.Config` nebo (liší se podle distribuce operačního systému) | Nastavení platí pro všechny operace, ale jsou přepsána všemi nastaveními na úrovni projektu. |
| Počítač | Windows:`%ProgramFiles(x86)%\NuGet\Config`<br/>Mac/Linux: `$XDG_DATA_HOME`. Pokud `$XDG_DATA_HOME` je null `~/.local/share` nebo `/usr/local/share` prázdné, nebo budou použity (se liší podle distribuce operačního systému)  | Nastavení platí pro všechny operace v počítači, ale jsou přepsána libovolným nastavením na úrovni uživatele nebo projektu. |

Poznámky k dřívějším verzím nugetu:
- NuGet 3.3 a `.nuget` starší používá složku pro nastavení celého řešení. Tato složka se nepoužívá v NuGet 3.4+.
- Pro soubor NuGet 2.6 až 3.x byl konfigurační soubor na úrovni počítače v\\systému Windows\\umístěn v\\%ProgramData%\NuGet\Config[ {IDE}[ {Version}[ {SKU}]]]\NuGet.Config, kde *{IDE}* může být *VisualStudio*, *{Version}* byla verze sady Visual Studio, například *14.0*, a *{SKU}* je *buď Community*, *Pro*, nebo *Enterprise*. Chcete-li migrovat nastavení do položky NuGet 4.0+, jednoduše zkopírujte konfigurační soubor do %ProgramFiles(x86)%\NuGet\Config. Na Linuxu bylo toto předchozí umístění /etc/opt a na Macu, /Library/Application Support.

## <a name="changing-config-settings"></a>Změna nastavení konfigurace

Soubor `NuGet.Config` je jednoduchý textový soubor XML obsahující páry klíč/hodnota, jak je popsáno v tématu [Nastavení konfigurace NuGet.](../reference/nuget-config-file.md)

Nastavení jsou spravována pomocí [příkazu konfigurace příkazu](../reference/cli-reference/cli-ref-config.md)NuGet CLI :
- Ve výchozím nastavení jsou změny v konfiguračním souboru na úrovni uživatele.
- Chcete-li změnit nastavení v `-configFile` jiném souboru, použijte přepínač. V tomto případě mohou soubory použít libovolný název souboru.
- Klíče jsou vždy rozlišována malá a velká písmena.
- Zvýšení oprávnění je nutné ke změně nastavení v souboru nastavení na úrovni počítače.

> [!Warning]
> Přestože můžete upravit soubor v libovolném textovém editoru, NuGet (v3.4.3 a novější) tiše ignoruje celý konfigurační soubor, pokud obsahuje poškozený XML (neodpovídající značky, neplatné uvozovky atd.). To je důvod, proč je vhodnější `nuget config`spravovat nastavení pomocí .

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
> V NuGet 3.4 a novější můžete použít proměnné prostředí `repositoryPath=%PACKAGEHOME%` v libovolné `repositoryPath=$PACKAGEHOME` hodnotě, jako v (Windows) a (Mac/Linux).

### <a name="removing-a-value"></a>Odebrání hodnoty

Chcete-li odebrat hodnotu, zadejte klíč s prázdnou hodnotou.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Vytvoření nového konfiguračního souboru

Zkopírujte níže uvedenou šablonu `nuget config -configFile <filename>` do nového souboru a pak nastavte hodnoty:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Jak se nastavení používají

Více `NuGet.Config` souborů umožňuje ukládat nastavení v různých umístěních tak, aby se vztahovaly na jeden projekt, skupinu projektů nebo všechny projekty. Tato nastavení společně platí pro všechny operace NuGet vyvolané z příkazového řádku nebo z Visual Studio, s nastavením, které existují "nejblíže" k projektu nebo aktuální složky s prioritou.

Konkrétně NuGet načte nastavení z různých konfiguračních souborů v následujícím pořadí:

1. [Soubor NuGetDefaults.Config](#nuget-defaults-file), který obsahuje nastavení související pouze se zdroji balíčků.
1. Soubor na úrovni počítače.
1. Soubor na úrovni uživatele.
1. Soubor zadaný `-configFile`pomocí aplikace .
1. Soubory nalezené v každé složce v cestě od kořenového adresáře jednotky k aktuální složce (kde je vyvolán nuget.exe nebo složka obsahující projekt sady Visual Studio). Pokud je například příkaz vyvolán v c:\A\B\C, společnost NuGet vyhledá a\, načte konfigurační soubory do c: potom c:\A, potom c:\A\B a nakonec c:\A\B\C.

Jako NuGet najde nastavení v těchto souborech, jsou použity takto:

1. Pro elementy s jednou položkou NuGet nahradil všechny dříve nalezené hodnoty pro stejný klíč. To znamená, že nastavení, která jsou "nejblíže" k aktuální složce nebo projektu přepsat všechny ostatní našel dříve. `defaultPushSource` Například nastavení in `NuGetDefaults.Config` je přepsáno, pokud existuje v jiném konfiguračním souboru.

1. Pro kolekce prvků `<packageSources>`(například ), NuGet kombinuje hodnoty ze všech konfiguračních souborů do jedné kolekce.

1. Pokud `<clear />` je k dispozici pro daný uzel, NuGet ignoruje dříve definované hodnoty konfigurace pro tento uzel.

### <a name="settings-walkthrough"></a>Návod k nastavení

Řekněme, že máte následující strukturu složek na dvou samostatných jednotkách:

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

Potom máte `NuGet.Config` čtyři soubory v následujících umístěních s daným obsahem. (Soubor na úrovni počítače není součástí tohoto příkladu, ale bude se chovat podobně jako soubor na úrovni uživatele.)

Soubor A. Soubor na`%appdata%\NuGet\NuGet.Config` úrovni uživatele, ( ve Windows, `~/.config/NuGet/NuGet.Config` na Mac/Linux):

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

Soubor D. disk_drive_2/Project2/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

NuGet pak načte a použije nastavení takto, v závislosti na tom, kde je vyvolána:

- **Vyvoláno z disk_drive_1/uživatelů**: Používá se pouze výchozí úložiště uvedené v konfiguračním souboru na úrovni uživatele (A), protože je to jediný soubor nalezený na disk_drive_1.

- **Vyvolána z disk_drive_2/ nebo disk_drive_/tmp**: Soubor na úrovni uživatele (A) je načten jako první, pak NuGet přejde do kořenového adresáře disk_drive_2 a najde soubor (B). NuGet také hledá konfigurační soubor v /tmp, ale nenajde jeden. V důsledku toho se používá výchozí úložiště na nuget.org, je povoleno obnovení balíčku a balíčky se rozbalí v disk_drive_2/tmp.

- **Vyvolána z disk_drive_2/Project1 nebo disk_drive_2/Project1/Source**: Soubor na úrovni uživatele (A) je načten jako první, potom NuGet načte soubor (B) z kořenového adresáře disk_drive_2, následovaný souborem (C). Nastavení v (C) přepsat ty v (B) `repositoryPath` a (A), takže kde se balíčky nainstalovat je disk_drive_2/Project1/External/Packages namísto *disk_drive_2/tmp*. Také proto, že (C) vymaže `<packageSources>`, `https://MyPrivateRepo/ES/nuget`nuget.org již není k dispozici jako zdroj, který ponechá pouze .

- **Vyvolána z disk_drive_2/Project2 nebo disk_drive_2/Project2/Source**: Soubor na úrovni uživatele (A) je načten nejprve následuje soubor (B) a soubor (D). Protože `packageSources` není vymazána, `nuget.org` `https://MyPrivateRepo/DQ/nuget` oba a jsou k dispozici jako zdroje. Balíčky se rozbalí v disk_drive_2/tmp, jak je uvedeno v (B).

## <a name="nuget-defaults-file"></a>NuGet výchozí soubor

Soubor `NuGetDefaults.Config` existuje, aby určil zdroje balíčků, ze kterých jsou balíčky nainstalovány `nuget push`a aktualizovány, a aby bylo nutné řídit výchozí cíl pro publikování balíčků pomocí aplikace . Vzhledem k tomu, že správci mohou pohodlně `NuGetDefaults.Config` (například pomocí zásad skupiny) nasadit konzistentní soubory do vývojářských a buildových počítačů, mohou zajistit, aby všichni v organizaci používali správné zdroje balíčků, nikoli nuget.org.

> [!Important]
> Soubor `NuGetDefaults.Config` nikdy způsobí, že zdroj balíčku, které mají být odebrány z konfigurace nuget vývojáře. To znamená, že pokud vývojář již použil NuGet a proto má nuget.org zdroj balíčku `NuGetDefaults.Config` registrován, nebude odebrán po vytvoření souboru.
>
> Kromě toho ani `NuGetDefaults.Config` žádný jiný mechanismus v NuGet můžete zabránit přístupu ke zdrojům balíčku, jako je nuget.org. Pokud organizace chce blokovat takový přístup, musí k tomu použít jiné prostředky, například brány firewall.

### <a name="nugetdefaultsconfig-location"></a>Umístění NuGetDefaults.Config

Následující tabulka popisuje, `NuGetDefaults.Config` kde by měl být soubor uložen v závislosti na cílovém os:

| Platforma Operačního eS  | Umístění NuGetDefaults.Config |
| --- | --- |
| Windows      | **Visual Studio 2017 nebo NuGet 4.x+:**`%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 a starší nebo NuGet 3.x a starší:**`%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME`(obvykle `~/.local/share` nebo `/usr/local/share`, v závislosti na distribuci Operačního systému)|

### <a name="nugetdefaultsconfig-settings"></a>Nastavení NuGetDefaults.Config

- `packageSources`: Tato kolekce má `packageSources` stejný význam jako v běžných konfiguračních souborech a určuje výchozí zdroje. NuGet používá zdroje v pořadí při instalaci nebo `packages.config` aktualizaci balíčků v projektech pomocí formátu pro správu. Pro projekty používající formát PackageReference nuget nejprve používá místní zdroje, pak zdroje na sdílené síťové složky, pak zdroje HTTP, bez ohledu na pořadí v konfiguračních souborech. NuGet vždy ignoruje pořadí zdrojů s operaceobnovení.

- `disabledPackageSources`: Tato kolekce má také `NuGet.Config` stejný význam jako v souborech, kde každý ohrožený zdroj je uveden podle jeho názvu a true/false hodnotu označující, zda je zakázán. To umožňuje, aby zdrojový název `packageSources` a adresa URL zůstaly ve výchozím nastavení, aniž by byly zapnuty. Jednotliví vývojáři pak mohou znovu povolit zdroj nastavením `NuGet.Config` hodnoty zdroje na false v jiných souborech, aniž by museli znovu najít správnou adresu URL. To je také užitečné pro poskytování vývojářům úplný seznam interních zdrojových adres URL pro organizaci a zároveň ve výchozím nastavení povolit pouze zdroj jednotlivých týmů.

- `defaultPushSource`: určuje výchozí cíl `nuget push` pro operace, přepsání předdefinované výchozí nuget.org. Správci mohou toto nastavení nasadit, aby se zabránilo publikování interních `nuget push -Source` balíčků na veřejné nuget.org náhodou, protože vývojáři konkrétně potřebují publikovat do nuget.org.

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
