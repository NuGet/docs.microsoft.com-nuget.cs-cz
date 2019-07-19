---
title: Běžné konfigurace NuGet
description: NuGet. config soubory řídí chování NuGet globálně i na jednotlivých projektech a jsou upraveny pomocí příkazu NuGet config.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 5309d94fafea9cdfc3699d443393be5d381dd145
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317732"
---
# <a name="common-nuget-configurations"></a>Běžné konfigurace NuGet

Chování NuGet se řídí seshromážděným nastavením v jednom nebo několika `NuGet.Config` souborech (XML), které můžou existovat na úrovni projektu, uživatele a počítače. Globální `NuGetDefaults.Config` soubor také konkrétně nakonfiguruje zdroje balíčků. Nastavení platí pro všechny příkazy vydávané v rozhraní příkazového řádku, konzole správce balíčků a uživatelské rozhraní Správce balíčků.

## <a name="config-file-locations-and-uses"></a>Umístění souborů konfigurace a použití

| Scope | Umístění souboru NuGet. config | Popis |
| --- | --- | --- |
| Řešení | Aktuální složka (neboli složka řešení) nebo libovolná složka až do kořenového adresáře jednotky.| Ve složce řešení se nastavení aplikuje na všechny projekty v podsložkách. Všimněte si, že pokud je konfigurační soubor umístěn ve složce projektu, nemá žádný vliv na tento projekt. |
| Uživatel | Windows: `%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux: `~/.config/NuGet/NuGet.Config` nebo `~/.nuget/NuGet/NuGet.Config` (liší se podle distribuce operačního systému) | Nastavení platí pro všechny operace, ale jsou přepsána všemi nastaveními na úrovni projektu. |
| Computer | Windows: `%ProgramFiles(x86)%\NuGet\Config`<br/>Mac/Linux: `$XDG_DATA_HOME`. Pokud `$XDG_DATA_HOME` má hodnotu null nebo je `~/.local/share` prázdný `/usr/local/share` , nebo se použije (liší se podle distribuce operačního systému)  | Nastavení platí pro všechny operace v počítači, ale jsou přepsána všemi uživateli nebo nastavením na úrovni projektu. |

Poznámky pro starší verze NuGet:
- NuGet 3,3 a starší používaly `.nuget` složku pro nastavení pro všechna řešení. Tento soubor se nepoužívá v NuGet 3.4 +.
- Pro NuGet 2,6 až 3. x je konfigurační soubor na úrovni počítače ve Windows umístěný v%ProgramData%\NuGet\Config\\[{IDE} [\\{Version} [\\{SKU}]]] \NuGet.config, kde *{IDE}* může být *VisualStudio*, *{ Verze}* byla verze sady Visual Studio, jako je například *14,0*, a *{SKU}* je *komunita*, *pro*nebo *podnik*. Chcete-li migrovat nastavení do NuGet 4.0 +, stačí zkopírovat konfigurační soubor do% ProgramFiles (x86)% \ NuGet\Config. V systému Linux se toto předchozí umístění/etc/opt a na Macu/Library/Application Support podpora.

## <a name="changing-config-settings"></a>Mění se nastavení konfigurace.

Soubor je jednoduchý textový soubor XML obsahující páry klíč/hodnota, jak je popsáno v tématu [nastavení konfigurace NuGet.](../reference/nuget-config-file.md) `NuGet.Config`

Nastavení se spravují pomocí příkazu NuGet CLI pro [konfiguraci](../reference/cli-reference/cli-ref-config.md):
- Ve výchozím nastavení se změny provedou v konfiguračním souboru na úrovni uživatele.
- Chcete-li změnit nastavení v jiném souboru, použijte `-configFile` přepínač. V tomto případě soubory můžou používat libovolný název souboru.
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
> V NuGet 3,4 a novějších můžete použít proměnné prostředí v libovolné hodnotě, jako v `repositoryPath=%PACKAGEHOME%` systému (Windows) `repositoryPath=$PACKAGEHOME` a (Mac/Linux).

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

Více `NuGet.Config` souborů vám umožňuje ukládat nastavení v různých umístěních, aby se mohla vztahovat na jeden projekt, skupinu projektů nebo všechny projekty. Tato nastavení se souhrnně vztahují na jakoukoliv operaci NuGet vyvolanou z příkazového řádku nebo ze sady Visual Studio s nastaveními, která existují "nejblíže" do projektu, nebo když aktuální složka převezme přednost.

Konkrétně NuGet načte nastavení z různých konfiguračních souborů v následujícím pořadí:

1. [Soubor NuGetDefaults. config](#nuget-defaults-file)obsahující nastavení související pouze se zdroji balíčků.
1. Soubor na úrovni počítače.
1. Soubor na úrovni uživatele.
1. Soubor zadaný pomocí `-configFile`.
1. Soubory nalezené v každé složce v cestě z kořene jednotky do aktuální složky (kde je vyvolán NuGet. exe nebo složka obsahující projekt sady Visual Studio). Například pokud je příkaz vyvolán v c:\A\B\C, NuGet vyhledá a načte konfigurační soubory v c:\, then c:\a, c:\A\B a finally c:\A\B\C.

Jelikož NuGet najde nastavení těchto souborů, použije se takto:

1. Pro prvky s jednou položkou nahradila NuGet všechny dříve nalezené hodnoty pro stejný klíč. To znamená, že nastavení, která jsou nejblíže aktuální složce nebo projektu, přepíší dříve nalezené. Například `defaultPushSource` nastavení v `NuGetDefaults.Config` je přepsáno, pokud existuje v jiném konfiguračním souboru.

1. Pro prvky kolekce (například `<packageSources>`) NuGet kombinuje hodnoty ze všech konfiguračních souborů do jedné kolekce.

1. Když `<clear />` je pro daný uzel k dispozici, NuGet ignoruje dříve definované hodnoty konfigurace pro tento uzel.

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

Pak budete mít k `NuGet.Config` danému obsahu čtyři soubory v následujících umístěních. (Soubor na úrovni počítače není v tomto příkladu zahrnutý, ale bude se chovat podobně jako soubor na úrovni uživatele.)

Soubor A. User-Level File (`%appdata%\NuGet\NuGet.Config` ve Windows, `~/.config/NuGet/NuGet.Config` na Mac/Linux):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

Soubor B. disk_drive_2/NuGet. config:

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

Soubor C. disk_drive_2/Project1/NuGet. config:

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

Soubor D. disk_drive_2/"Project2"/NuGet. config:

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

- **Vyvoláno z disk_drive_1/uživatelů**: Použije se jenom výchozí úložiště uvedené v konfiguračním souboru na úrovni uživatele (A), protože to je jediný soubor, který najdete na disk_drive_1.

- **Vyvoláno z disk_drive_2/nebo disk_drive_/TMP**: Nejprve se načte soubor na úrovni uživatele (A), potom NuGet přejde do kořenového adresáře disk_drive_2 a vyhledá soubor (B). NuGet také hledá konfigurační soubor v adresáře/TMP, ale nenalezne ho. V důsledku toho se použije výchozí úložiště v nuget.org, obnovení balíčku je povolené a balíčky se rozšiřují v disk_drive_2/TMP.

- **Vyvoláno z disk_drive_2/Project1 nebo disk_drive_2/Project1/source**: Nejprve se načte soubor na úrovni uživatele (A) a potom NuGet načte soubor (B) z kořenového adresáře disk_drive_2 a pak podle souboru (C). Nastavení v (C) přepíší tyto položky v (B) a (A), `repositoryPath` takže balíčky, kde se nainstalují balíčky, jsou disk_drive_2/Project1/External/Packages místo *disk_drive_2/TMP*. V důsledku toho, že (C) `<packageSources>`vymazání, NuGet.org již není k dispozici jako zdroj `https://MyPrivateRepo/ES/nuget`opouští.

- **Vyvoláno z disk_drive_2/"Project2" nebo disk_drive_2/"Project2"/Source**: Soubor na úrovni uživatele (A) se načte za prvé a pak na soubor (B) a soubor (D). Vzhledem `packageSources` k tomu `nuget.org` , že není zaškrtnuté, a `https://MyPrivateRepo/DQ/nuget` jsou k dispozici jako zdroje. Balíčky se rozšiřují v disk_drive_2/TMP, jak je uvedeno v (B).

## <a name="nuget-defaults-file"></a>Soubor výchozích hodnot NuGet

Soubor existuje za účelem určení zdrojů balíčků, ze kterých jsou balíčky nainstalovány a aktualizovány, a pro kontrolu výchozího cíle pro publikování balíčků pomocí `nuget push`. `NuGetDefaults.Config` Vzhledem k tomu, že správci můžou pohodlně (například pomocí Zásady skupiny) nasazovat konzistentní `NuGetDefaults.Config` soubory do počítačů pro vývojáře a sestavování, můžou zajistit, aby všichni v organizaci používali místo NuGet.org správné zdroje balíčků.

> [!Important]
> `NuGetDefaults.Config` Soubor nikdy nezpůsobí odebrání zdroje balíčku z konfigurace NuGet vývojáře. To znamená, že pokud vývojář již použil NuGet, a proto má registrovaný zdroj balíčku NuGet.org, po vytvoření `NuGetDefaults.Config` souboru se neodstraní.
>
> `NuGetDefaults.Config` Navíc ani žádný jiný mechanismus v NuGet nemůže zabránit přístupu ke zdrojům balíčků, jako je NuGet.org. Pokud si organizace chce takový přístup zablokovat, musí k tomu použít jiné prostředky, jako například brány firewall.

### <a name="nugetdefaultsconfig-location"></a>Umístění NuGetDefaults. config

Následující tabulka popisuje, kde `NuGetDefaults.Config` by měl být soubor uložený v závislosti na cílovém operačním systému:

| Platforma operačního systému  | Umístění NuGetDefaults. config |
| --- | --- |
| Windows      | **Visual Studio 2017 nebo NuGet 4. x +:** `%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 a starší nebo NuGet 3. x a starší:** `%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME`(obvykle `~/.local/share` nebo `/usr/local/share`, v závislosti na distribuci operačního systému)|

### <a name="nugetdefaultsconfig-settings"></a>Nastavení NuGetDefaults. config

- `packageSources`: Tato kolekce má stejný význam jako v `packageSources` případě běžných konfiguračních souborů a určuje výchozí zdroje. Nástroj NuGet používá zdroje v pořadí při instalaci nebo aktualizaci balíčků v projektech pomocí `packages.config` formátu správy. Pro projekty, které používají formát PackageReference, NuGet používá nejprve místní zdroje, pak zdroje na sdílených síťových složkách a pak zdroje HTTP bez ohledu na pořadí v konfiguračních souborech. NuGet vždycky ignoruje pořadí zdrojů s operacemi obnovení.

- `disabledPackageSources`: Tato kolekce má také stejný význam jako v `NuGet.Config` souborech, kde je každý ovlivněný zdroj uveden podle názvu a hodnota true/false, která označuje, jestli je zakázaná. Tím umožníte, aby název zdroje a adresa URL `packageSources` zůstaly v neaktivním stavu, aniž by bylo ve výchozím nastavení zapnuté. Jednotliví vývojáři potom můžou zdroj znovu povolit nastavením hodnoty zdroje na hodnotu false v jiných `NuGet.Config` souborech, aniž by museli znovu najít správnou adresu URL. To je užitečné také k tomu, aby vývojářům poskytoval úplný seznam interních zdrojových adres URL pro organizaci, přičemž ve výchozím nastavení povoluje pouze zdroj jednotlivých týmů.

- `defaultPushSource`: Určuje výchozí cíl pro `nuget push` operace a přepíše vestavěnou výchozí hodnotu NuGet.org. Správci můžou toto nastavení nasadit, aby nedocházelo k publikování interních balíčků na veřejné NuGet.org po havárii, protože vývojáři potřebují `nuget push -Source` použít k publikování na NuGet.org.

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
