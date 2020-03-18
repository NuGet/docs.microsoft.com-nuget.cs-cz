---
title: Běžné konfigurace NuGet
description: NuGet. config soubory řídí chování NuGet globálně i na jednotlivých projektech a jsou upraveny pomocí příkazu NuGet config.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 89127203df0aa1eb24f36b8ec64c5bb4a4d59319
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428910"
---
# <a name="common-nuget-configurations"></a>Běžné konfigurace NuGet

Chování NuGet se řídí seshromážděným nastavením v jednom nebo několika souborech `NuGet.Config` (XML), které můžou existovat na úrovni projektu, uživatele a počítače. Globální `NuGetDefaults.Config` soubor také konkrétně nakonfiguruje zdroje balíčků. Nastavení platí pro všechny příkazy vydávané v rozhraní příkazového řádku, konzole správce balíčků a uživatelské rozhraní Správce balíčků.

## <a name="config-file-locations-and-uses"></a>Umístění souborů konfigurace a použití

| Rozsah | Umístění souboru NuGet. config | Popis |
| --- | --- | --- |
| Řešení | Aktuální složka (neboli složka řešení) nebo libovolná složka až do kořenového adresáře jednotky.| Ve složce řešení se nastavení aplikuje na všechny projekty v podsložkách. Všimněte si, že pokud je konfigurační soubor umístěn ve složce projektu, nemá žádný vliv na tento projekt. |
| Uživatel | Windows: `%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux: `~/.config/NuGet/NuGet.Config` nebo `~/.nuget/NuGet/NuGet.Config` (liší se podle distribuce operačního systému) | Nastavení platí pro všechny operace, ale jsou přepsána všemi nastaveními na úrovni projektu. |
| Počítač | Windows: `%ProgramFiles(x86)%\NuGet\Config`<br/>Mac/Linux: `$XDG_DATA_HOME`. Pokud `$XDG_DATA_HOME` má hodnotu null nebo je prázdné, bude použita `~/.local/share` nebo `/usr/local/share` (liší se podle distribuce operačního systému).  | Nastavení platí pro všechny operace v počítači, ale jsou přepsána všemi uživateli nebo nastavením na úrovni projektu. |

Poznámky pro starší verze NuGet:
- NuGet 3,3 a starší používaly `.nuget` složku pro nastavení pro všechna řešení. Tato složka se nepoužívá v NuGet 3.4 +.
- Pro NuGet 2,6 až 3. x byl konfigurační soubor na úrovni počítače ve Windows umístěný v%ProgramData%\NuGet\Config [\\{IDE} [\\{Version} [\\{SKU}]]] \NuGet.Config, kde *{IDE}* může být *VisualStudio*, *{Version}* byla verze sady Visual Studio, jako je *14,0*a *{SKU}* je *komunita*, *pro*nebo *podnik*. Chcete-li migrovat nastavení do NuGet 4.0 +, stačí zkopírovat konfigurační soubor do% ProgramFiles (x86)% \ NuGet\Config. V systému Linux se toto předchozí umístění/etc/opt a na Macu/Library/Application Support podpora.

## <a name="changing-config-settings"></a>Mění se nastavení konfigurace.

Soubor `NuGet.Config` je jednoduchý textový soubor XML obsahující páry klíč/hodnota, jak je popsáno v tématu [nastavení konfigurace NuGet](../reference/nuget-config-file.md) .

Nastavení se spravují pomocí příkazu NuGet CLI pro [konfiguraci](../reference/cli-reference/cli-ref-config.md):
- Ve výchozím nastavení se změny provedou v konfiguračním souboru na úrovni uživatele.
- Chcete-li změnit nastavení v jiném souboru, použijte přepínač `-configFile`. V tomto případě soubory můžou používat libovolný název souboru.
- U klíčů se rozlišují malá a velká písmena.
- Ke změně nastavení v souboru nastavení na úrovni počítače je potřeba zvýšení oprávnění.

> [!Warning]
> I když můžete soubor upravovat v libovolném textovém editoru, NuGet (v 3.4.3 a novějším) tiše ignoruje celý konfigurační soubor, pokud obsahuje nesprávně vytvořený kód XML (neshodné značky, neplatné uvozovky atd.). To je důvod, proč je vhodnější spravovat nastavení pomocí `nuget config`.

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
> V NuGet 3,4 a novějších můžete použít proměnné prostředí v libovolné hodnotě, jako v `repositoryPath=%PACKAGEHOME%` (Windows) a `repositoryPath=$PACKAGEHOME` (Mac/Linux).

### <a name="removing-a-value"></a>Odebrání hodnoty

Chcete-li odebrat hodnotu, zadejte klíč s prázdnou hodnotou.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Vytváření nového konfiguračního souboru

Zkopírujte níže uvedenou šablonu do nového souboru a pak použijte `nuget config -configFile <filename>` k nastavení hodnot:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Způsob použití nastavení

Více `NuGet.Config` souborů vám umožní ukládat nastavení v různých umístěních, aby se mohla vztahovat na jeden projekt, skupinu projektů nebo všechny projekty. Tato nastavení se souhrnně vztahují na jakoukoliv operaci NuGet vyvolanou z příkazového řádku nebo ze sady Visual Studio s nastaveními, která existují "nejblíže" do projektu, nebo když aktuální složka převezme přednost.

Konkrétně NuGet načte nastavení z různých konfiguračních souborů v následujícím pořadí:

1. [Soubor NuGetDefaults. config](#nuget-defaults-file)obsahující nastavení související pouze se zdroji balíčků.
1. Soubor na úrovni počítače.
1. Soubor na úrovni uživatele.
1. Soubor zadaný pomocí `-configFile`.
1. Soubory nalezené v každé složce v cestě z kořene jednotky do aktuální složky (kde je vyvolán NuGet. exe nebo složka obsahující projekt sady Visual Studio). Například pokud je příkaz vyvolán v c:\A\B\C, NuGet vyhledá a načte konfigurační soubory v jazyce c:\, potom c:\A, c:\A\B a finally c:\A\B\C.

Jelikož NuGet najde nastavení těchto souborů, použije se takto:

1. Pro prvky s jednou položkou nahradila NuGet všechny dříve nalezené hodnoty pro stejný klíč. To znamená, že nastavení, která jsou nejblíže aktuální složce nebo projektu, přepíší dříve nalezené. Například nastavení `defaultPushSource` v `NuGetDefaults.Config` je přepsáno, pokud existuje v jiném konfiguračním souboru.

1. Pro prvky kolekce (například `<packageSources>`) NuGet kombinuje hodnoty ze všech konfiguračních souborů do jedné kolekce.

1. Pokud je pro daný uzel k dispozici `<clear />`, NuGet ignoruje dříve definované hodnoty konfigurace pro tento uzel.

### <a name="settings-walkthrough"></a>Návod k nastavení

Řekněme, že máte na dvou samostatných jednotkách tuto strukturu složek:

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

Pak budete mít čtyři `NuGet.Config` soubory v následujících umístěních s daným obsahem. (Soubor na úrovni počítače není v tomto příkladu zahrnutý, ale bude se chovat podobně jako soubor na úrovni uživatele.)

Soubor A. User-Level File (`%appdata%\NuGet\NuGet.Config` ve Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

Soubor B disk_drive_2/NuGet.Config:

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

NuGet potom načte a aplikuje nastavení podle toho, kde se vyvolalo:

- **Vyvoláno z disk_drive_1/Users**: používá se jenom výchozí úložiště uvedené v konfiguračním souboru na úrovni uživatele (A), protože to je jediný soubor, který se nachází v disk_drive_1.

- **Vyvoláno z disk_drive_2/nebo disk_drive_ adresáře/TMP**: nejprve se načte soubor na úrovni uživatele (a), pak NuGet přejde do kořenového adresáře disk_drive_2 a vyhledá soubor (B). NuGet také hledá konfigurační soubor v adresáře/TMP, ale nenalezne ho. V důsledku toho se použije výchozí úložiště v nuget.org, je povolené obnovení balíčků a balíčky se rozbalí v disk_drive_2/TMP.

- **Vyvoláno z disk_drive_2/Project1 nebo disk_drive_2/Project1/source**: nejprve se načte soubor na úrovni uživatele (A), pak NuGet načte soubor (B) z kořenového adresáře disk_drive_2 následovaný souborem (C). Nastavení v (C) přepíší ta v (B) a (A), takže `repositoryPath`, kde se balíčky nainstalují, disk_drive_2/Project1/External/Packages místo *disk_drive_2 adresáře/TMP*. Z toho důvodu, že (C) vymaže `<packageSources>`nuget.org, již není k dispozici jako zdroj, který opouští pouze `https://MyPrivateRepo/ES/nuget`.

- **Vyvoláno z disk_drive_2/Project2 nebo disk_drive_2/Project2/source**: soubor na úrovni uživatele (A) se načte za prvé následovaný souborem (B) a souborem (D). Vzhledem k tomu, že `packageSources` není zaškrtnuto, jsou jako zdroje k dispozici `nuget.org` a `https://MyPrivateRepo/DQ/nuget`. Balíčky se rozšiřují v disk_drive_2 adresáře/TMP, jak je uvedeno v (B).

## <a name="nuget-defaults-file"></a>Soubor výchozích hodnot NuGet

`NuGetDefaults.Config` soubor existuje, chcete-li určit zdroje balíčků, ze kterých jsou balíčky nainstalovány a aktualizovány, a řídit výchozí cíl pro publikování balíčků pomocí `nuget push`. Vzhledem k tomu, že správci můžou pohodlně (například pomocí Zásady skupiny) nasazovat konzistentní `NuGetDefaults.Config` soubory pro vývojáře a sestavování počítačů, můžou zajistit, aby všichni v organizaci používali místo nuget.org správné zdroje balíčků.

> [!Important]
> `NuGetDefaults.Config` soubor nikdy nezpůsobí odebrání zdroje balíčku z konfigurace NuGet vývojáře. To znamená, že pokud vývojář již použil NuGet, a proto má registrovaný zdroj balíčku nuget.org, nebude po vytvoření souboru `NuGetDefaults.Config` odebrán.
>
> Kromě toho ani `NuGetDefaults.Config` ani žádný jiný mechanismus v NuGet nemůže zabránit přístupu ke zdrojům balíčků, jako je nuget.org. Pokud si organizace chce takový přístup zablokovat, musí k tomu použít jiné prostředky, jako například brány firewall.

### <a name="nugetdefaultsconfig-location"></a>Umístění NuGetDefaults. config

Následující tabulka popisuje, kde by měl být soubor `NuGetDefaults.Config` uložený v závislosti na cílovém operačním systému:

| Platforma operačního systému  | Umístění NuGetDefaults. config |
| --- | --- |
| Windows      | **Visual Studio 2017 nebo NuGet 4. x +:** `%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 a starší nebo NuGet 3. x a starší:** `%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME` (obvykle `~/.local/share` nebo `/usr/local/share`v závislosti na distribuci operačního systému)|

### <a name="nugetdefaultsconfig-settings"></a>Nastavení NuGetDefaults. config

- `packageSources`: Tato kolekce má stejný význam jako `packageSources` v běžných konfiguračních souborech a určuje výchozí zdroje. Nástroj NuGet používá zdroje v pořadí při instalaci nebo aktualizaci balíčků v projektech pomocí formátu správy `packages.config`. Pro projekty, které používají formát PackageReference, NuGet používá nejprve místní zdroje, pak zdroje na sdílených síťových složkách a pak zdroje HTTP bez ohledu na pořadí v konfiguračních souborech. NuGet vždycky ignoruje pořadí zdrojů s operacemi obnovení.

- `disabledPackageSources`: Tato kolekce má také stejný význam jako v souborech `NuGet.Config`, kde je každý ovlivněný zdroj uveden podle názvu a hodnota true/false, která označuje, jestli je zakázaná. To umožňuje, aby název zdroje a adresa URL zůstaly v `packageSources`, aniž by bylo ve výchozím nastavení zapnuté. Jednotliví vývojáři potom můžou zdroj znovu povolit nastavením hodnoty zdroje na hodnotu false v jiných `NuGet.Config` souborech, aniž by museli znovu najít správnou adresu URL. To je užitečné také k tomu, aby vývojářům poskytoval úplný seznam interních zdrojových adres URL pro organizaci, přičemž ve výchozím nastavení povoluje pouze zdroj jednotlivých týmů.

- `defaultPushSource`: Určuje výchozí cíl pro operace `nuget push` a přepíše vestavěnou výchozí hodnotu nuget.org. Správci můžou toto nastavení nasadit, aby nedocházelo k publikování interních balíčků na veřejném nuget.orgu po havárii, protože vývojáři potřebují k publikování do nuget.org použít `nuget push -Source`.

### <a name="example-nugetdefaultsconfig-and-application"></a>Příklad NuGetDefaults. config a Application

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
