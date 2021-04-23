---
title: Běžné konfigurace NuGetu
description: NuGet.Config soubory NuGet řídí chování NuGet globálně i na jednotlivých projektech a jsou upraveny pomocí příkazu NuGet config.
author: JonDouglas
ms.author: jodou
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 18e3af7145495b5753b5900915ffb4b07942b856
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901470"
---
# <a name="common-nuget-configurations"></a><span data-ttu-id="5fd30-103">Běžné konfigurace NuGetu</span><span class="sxs-lookup"><span data-stu-id="5fd30-103">Common NuGet configurations</span></span>

<span data-ttu-id="5fd30-104">Chování NuGet se řídí seshromážděným nastavením v jednom nebo několika `NuGet.Config` souborech (XML), které můžou existovat na úrovni projektu, uživatele a počítače.</span><span class="sxs-lookup"><span data-stu-id="5fd30-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="5fd30-105">Globální `NuGetDefaults.Config` soubor také konkrétně nakonfiguruje zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="5fd30-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="5fd30-106">Nastavení platí pro všechny příkazy vydávané v rozhraní příkazového řádku, konzole správce balíčků a uživatelské rozhraní Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="5fd30-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="5fd30-107">Umístění souborů konfigurace a použití</span><span class="sxs-lookup"><span data-stu-id="5fd30-107">Config file locations and uses</span></span>

| <span data-ttu-id="5fd30-108">Obor</span><span class="sxs-lookup"><span data-stu-id="5fd30-108">Scope</span></span> | <span data-ttu-id="5fd30-109">`NuGet.Config` umístění souboru</span><span class="sxs-lookup"><span data-stu-id="5fd30-109">`NuGet.Config` file location</span></span> | <span data-ttu-id="5fd30-110">Popis</span><span class="sxs-lookup"><span data-stu-id="5fd30-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5fd30-111">Řešení</span><span class="sxs-lookup"><span data-stu-id="5fd30-111">Solution</span></span> | <span data-ttu-id="5fd30-112">Aktuální složka (neboli složka řešení) nebo libovolná složka až do kořenového adresáře jednotky.</span><span class="sxs-lookup"><span data-stu-id="5fd30-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="5fd30-113">Ve složce řešení se nastavení aplikuje na všechny projekty v podsložkách.</span><span class="sxs-lookup"><span data-stu-id="5fd30-113">In a solution folder, settings apply to all projects in subfolders.</span></span> <span data-ttu-id="5fd30-114">Všimněte si, že pokud je konfigurační soubor umístěn ve složce projektu, nemá žádný vliv na tento projekt.</span><span class="sxs-lookup"><span data-stu-id="5fd30-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="5fd30-115">Uživatel</span><span class="sxs-lookup"><span data-stu-id="5fd30-115">User</span></span> | <span data-ttu-id="5fd30-116">**Windows:**`%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="5fd30-116">**Windows:** `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="5fd30-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` nebo `~/.nuget/NuGet/NuGet.Config` (se liší distribucí operačního systému)</span><span class="sxs-lookup"><span data-stu-id="5fd30-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> <br/><span data-ttu-id="5fd30-118">Další konfigurace jsou podporované na všech platformách.</span><span class="sxs-lookup"><span data-stu-id="5fd30-118">Additional configs are supported on all platforms.</span></span> <span data-ttu-id="5fd30-119">Tyto konfigurace nelze upravovat pomocí nástrojů.</span><span class="sxs-lookup"><span data-stu-id="5fd30-119">These configs cannot be edited by the tooling.</span></span> </br> <span data-ttu-id="5fd30-120">**Windows:**`%appdata%\NuGet\config\*.Config`</span><span class="sxs-lookup"><span data-stu-id="5fd30-120">**Windows:** `%appdata%\NuGet\config\*.Config`</span></span> <br/><span data-ttu-id="5fd30-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` ani `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="5fd30-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> | <span data-ttu-id="5fd30-122">Nastavení platí pro všechny operace, ale jsou přepsána všemi nastaveními na úrovni projektu.</span><span class="sxs-lookup"><span data-stu-id="5fd30-122">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="5fd30-123">Počítač</span><span class="sxs-lookup"><span data-stu-id="5fd30-123">Computer</span></span> | <span data-ttu-id="5fd30-124">**Windows:**`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="5fd30-124">**Windows:** `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="5fd30-125">**Mac/Linux:** `$XDG_DATA_HOME` .</span><span class="sxs-lookup"><span data-stu-id="5fd30-125">**Mac/Linux:** `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="5fd30-126">Pokud `$XDG_DATA_HOME` má hodnotu null nebo je prázdný, `~/.local/share` nebo se `/usr/local/share` použije (liší se podle distribuce operačního systému)</span><span class="sxs-lookup"><span data-stu-id="5fd30-126">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="5fd30-127">Nastavení platí pro všechny operace v počítači, ale jsou přepsána všemi uživateli nebo nastavením na úrovni projektu.</span><span class="sxs-lookup"><span data-stu-id="5fd30-127">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="5fd30-128">Poznámky pro starší verze NuGet:</span><span class="sxs-lookup"><span data-stu-id="5fd30-128">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="5fd30-129">NuGet 3,3 a starší používaly `.nuget` složku pro nastavení pro všechna řešení.</span><span class="sxs-lookup"><span data-stu-id="5fd30-129">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="5fd30-130">Tato složka se nepoužívá v NuGet 3.4 +.</span><span class="sxs-lookup"><span data-stu-id="5fd30-130">This folder is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="5fd30-131">V případě NuGet 2,6 až 3. x se v systému Windows nachází konfigurační soubor na úrovni počítače `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]\NuGet.Config` , ve kterém se `{IDE}` může `VisualStudio` jednat `{Version}` o verzi sady Visual Studio, jako je například `14.0` , a `{SKU}` je buď `Community` , `Pro` nebo `Enterprise` .</span><span class="sxs-lookup"><span data-stu-id="5fd30-131">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]\NuGet.Config`, where `{IDE}` can be `VisualStudio`, `{Version}` was the Visual Studio version such as `14.0`, and `{SKU}` is either `Community`, `Pro`, or `Enterprise`.</span></span> <span data-ttu-id="5fd30-132">Chcete-li migrovat nastavení do NuGet 4.0 +, stačí zkopírovat konfigurační soubor do `%ProgramFiles(x86)%\NuGet\Config` .</span><span class="sxs-lookup"><span data-stu-id="5fd30-132">To migrate settings to NuGet 4.0+, simply copy the config file to `%ProgramFiles(x86)%\NuGet\Config`.</span></span> <span data-ttu-id="5fd30-133">V systému Linux se jednalo o toto předchozí umístění `/etc/opt` a na Macu `/Library/Application Support` .</span><span class="sxs-lookup"><span data-stu-id="5fd30-133">On Linux, this previous location was `/etc/opt`, and on Mac, `/Library/Application Support`.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="5fd30-134">Mění se nastavení konfigurace.</span><span class="sxs-lookup"><span data-stu-id="5fd30-134">Changing config settings</span></span>

<span data-ttu-id="5fd30-135">`NuGet.Config`Soubor je jednoduchý textový soubor XML obsahující páry klíč/hodnota, jak je popsáno v tématu [nastavení konfigurace NuGet](../reference/nuget-config-file.md) .</span><span class="sxs-lookup"><span data-stu-id="5fd30-135">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="5fd30-136">Nastavení se spravují pomocí příkazu NuGet CLI pro [konfiguraci](../reference/cli-reference/cli-ref-config.md):</span><span class="sxs-lookup"><span data-stu-id="5fd30-136">Settings are managed using the NuGet CLI [config command](../reference/cli-reference/cli-ref-config.md):</span></span>
- <span data-ttu-id="5fd30-137">Ve výchozím nastavení se změny provedou v konfiguračním souboru na úrovni uživatele.</span><span class="sxs-lookup"><span data-stu-id="5fd30-137">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="5fd30-138">Chcete-li změnit nastavení v jiném souboru, použijte `-configFile` přepínač.</span><span class="sxs-lookup"><span data-stu-id="5fd30-138">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="5fd30-139">V tomto případě soubory můžou používat libovolný název souboru.</span><span class="sxs-lookup"><span data-stu-id="5fd30-139">In this case files can use any filename.</span></span>
- <span data-ttu-id="5fd30-140">U klíčů se rozlišují malá a velká písmena.</span><span class="sxs-lookup"><span data-stu-id="5fd30-140">Keys are always case sensitive.</span></span>
- <span data-ttu-id="5fd30-141">Ke změně nastavení v souboru nastavení na úrovni počítače je potřeba zvýšení oprávnění.</span><span class="sxs-lookup"><span data-stu-id="5fd30-141">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="5fd30-142">I když můžete soubor upravovat v libovolném textovém editoru, NuGet (v 3.4.3 a novějším) tiše ignoruje celý konfigurační soubor, pokud obsahuje nesprávně vytvořený kód XML (neshodné značky, neplatné uvozovky atd.).</span><span class="sxs-lookup"><span data-stu-id="5fd30-142">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="5fd30-143">To je důvod, proč je vhodnější spravovat nastavení pomocí `nuget config` .</span><span class="sxs-lookup"><span data-stu-id="5fd30-143">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="5fd30-144">Nastavení hodnoty</span><span class="sxs-lookup"><span data-stu-id="5fd30-144">Setting a value</span></span>

<span data-ttu-id="5fd30-145">Windows:</span><span class="sxs-lookup"><span data-stu-id="5fd30-145">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="5fd30-146">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="5fd30-146">Mac/Linux:</span></span>

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
> <span data-ttu-id="5fd30-147">V NuGet 3,4 a novějších můžete použít proměnné prostředí v libovolné hodnotě, jako v `repositoryPath=%PACKAGEHOME%` systému (Windows) a `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5fd30-147">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="5fd30-148">Odebrání hodnoty</span><span class="sxs-lookup"><span data-stu-id="5fd30-148">Removing a value</span></span>

<span data-ttu-id="5fd30-149">Chcete-li odebrat hodnotu, zadejte klíč s prázdnou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="5fd30-149">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="5fd30-150">Vytváření nového konfiguračního souboru</span><span class="sxs-lookup"><span data-stu-id="5fd30-150">Creating a new config file</span></span>

<span data-ttu-id="5fd30-151">Zkopírujte níže uvedenou šablonu do nového souboru a pak použijte `nuget config -configFile <filename>` k nastavení hodnot:</span><span class="sxs-lookup"><span data-stu-id="5fd30-151">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="5fd30-152">Způsob použití nastavení</span><span class="sxs-lookup"><span data-stu-id="5fd30-152">How settings are applied</span></span>

<span data-ttu-id="5fd30-153">Více `NuGet.Config` souborů vám umožňuje ukládat nastavení v různých umístěních, aby se mohla vztahovat na jeden projekt, skupinu projektů nebo všechny projekty.</span><span class="sxs-lookup"><span data-stu-id="5fd30-153">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="5fd30-154">Tato nastavení se souhrnně vztahují na jakoukoliv operaci NuGet vyvolanou z příkazového řádku nebo ze sady Visual Studio s nastaveními, která existují "nejblíže" do projektu, nebo když aktuální složka převezme přednost.</span><span class="sxs-lookup"><span data-stu-id="5fd30-154">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="5fd30-155">Konkrétně NuGet načte nastavení z různých konfiguračních souborů v následujícím pořadí:</span><span class="sxs-lookup"><span data-stu-id="5fd30-155">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="5fd30-156">[ `NuGetDefaults.Config` Soubor](#nuget-defaults-file), který obsahuje nastavení související pouze se zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="5fd30-156">The [`NuGetDefaults.Config` file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="5fd30-157">Soubor na úrovni počítače.</span><span class="sxs-lookup"><span data-stu-id="5fd30-157">The computer-level file.</span></span>
1. <span data-ttu-id="5fd30-158">Soubor na úrovni uživatele.</span><span class="sxs-lookup"><span data-stu-id="5fd30-158">The user-level file.</span></span>
1. <span data-ttu-id="5fd30-159">Soubor zadaný pomocí `-configFile` .</span><span class="sxs-lookup"><span data-stu-id="5fd30-159">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="5fd30-160">Soubory nalezené v každé složce v cestě z kořene jednotky do aktuální složky (kde `nuget.exe` je vyvolána nebo složka obsahující projekt sady Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="5fd30-160">Files found in every folder in the path from the drive root to the current folder (where `nuget.exe` is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="5fd30-161">Například pokud je příkaz vyvolán v `c:\A\B\C` , NuGet vyhledá a načte konfigurační soubory v `c:\` , pak, `c:\A` `c:\A\B` a nakonec `c:\A\B\C` .</span><span class="sxs-lookup"><span data-stu-id="5fd30-161">For example, if a command is invoked in `c:\A\B\C`, NuGet looks for and loads config files in `c:\`, then `c:\A`, then `c:\A\B`, and finally `c:\A\B\C`.</span></span>

<span data-ttu-id="5fd30-162">Jelikož NuGet najde nastavení těchto souborů, použije se takto:</span><span class="sxs-lookup"><span data-stu-id="5fd30-162">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="5fd30-163">Pro prvky s jednou položkou nahradila NuGet všechny dříve nalezené hodnoty pro stejný klíč.</span><span class="sxs-lookup"><span data-stu-id="5fd30-163">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="5fd30-164">To znamená, že nastavení, která jsou nejblíže aktuální složce nebo projektu, přepíší dříve nalezené.</span><span class="sxs-lookup"><span data-stu-id="5fd30-164">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="5fd30-165">Například `defaultPushSource` nastavení v `NuGetDefaults.Config` je přepsáno, pokud existuje v jiném konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="5fd30-165">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>
1. <span data-ttu-id="5fd30-166">Pro prvky kolekce (například `<packageSources>` ) NuGet kombinuje hodnoty ze všech konfiguračních souborů do jedné kolekce.</span><span class="sxs-lookup"><span data-stu-id="5fd30-166">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>
1. <span data-ttu-id="5fd30-167">Když `<clear />` je pro daný uzel k dispozici, NuGet ignoruje dříve definované hodnoty konfigurace pro tento uzel.</span><span class="sxs-lookup"><span data-stu-id="5fd30-167">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="5fd30-168">Návod k nastavení</span><span class="sxs-lookup"><span data-stu-id="5fd30-168">Settings walkthrough</span></span>

<span data-ttu-id="5fd30-169">Řekněme, že máte na dvou samostatných jednotkách tuto strukturu složek:</span><span class="sxs-lookup"><span data-stu-id="5fd30-169">Let's say you have the following folder structure on two separate drives:</span></span>

```
disk_drive_1
    User
disk_drive_2
    Project1
        Source
    Project2
        Source
    tmp
```

<span data-ttu-id="5fd30-170">Pak budete mít k `NuGet.Config` danému obsahu čtyři soubory v následujících umístěních.</span><span class="sxs-lookup"><span data-stu-id="5fd30-170">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="5fd30-171">(Soubor na úrovni počítače není v tomto příkladu zahrnutý, ale bude se chovat podobně jako soubor na úrovni uživatele.)</span><span class="sxs-lookup"><span data-stu-id="5fd30-171">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="5fd30-172">Soubor A. User-Level File ( `%appdata%\NuGet\NuGet.Config` ve Windows, `~/.config/NuGet/NuGet.Config` na Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="5fd30-172">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="5fd30-173">Soubor B `disk_drive_2/NuGet.Config` :</span><span class="sxs-lookup"><span data-stu-id="5fd30-173">File B. `disk_drive_2/NuGet.Config`:</span></span>

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

<span data-ttu-id="5fd30-174">Soubor C `disk_drive_2/Project1/NuGet.Config` :</span><span class="sxs-lookup"><span data-stu-id="5fd30-174">File C. `disk_drive_2/Project1/NuGet.Config`:</span></span>

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

<span data-ttu-id="5fd30-175">Soubor D. `disk_drive_2/Project2/NuGet.Config` :</span><span class="sxs-lookup"><span data-stu-id="5fd30-175">File D. `disk_drive_2/Project2/NuGet.Config`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="5fd30-176">NuGet potom načte a aplikuje nastavení podle toho, kde se vyvolalo:</span><span class="sxs-lookup"><span data-stu-id="5fd30-176">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="5fd30-177">**Vyvoláno z `disk_drive_1/users`**: používá se jenom výchozí úložiště uvedené v konfiguračním souboru na úrovni uživatele (A), protože to je jediný soubor, na kterém se nachází `disk_drive_1` .</span><span class="sxs-lookup"><span data-stu-id="5fd30-177">**Invoked from `disk_drive_1/users`**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on `disk_drive_1`.</span></span>

- <span data-ttu-id="5fd30-178">**Vyvoláno z `disk_drive_2/` nebo `disk_drive_/tmp`**: nejprve se načte soubor na úrovni uživatele (a), pak NuGet přejde do kořenové složky `disk_drive_2` a vyhledá soubor (B).</span><span class="sxs-lookup"><span data-stu-id="5fd30-178">**Invoked from `disk_drive_2/` or `disk_drive_/tmp`**: The user-level file (A) is loaded first, then NuGet goes to the root of `disk_drive_2` and finds file (B).</span></span> <span data-ttu-id="5fd30-179">NuGet také hledá konfigurační soubor v, `/tmp` ale nenalezne ho.</span><span class="sxs-lookup"><span data-stu-id="5fd30-179">NuGet also looks for a configuration file in `/tmp` but does not find one.</span></span> <span data-ttu-id="5fd30-180">V důsledku toho se používá výchozí úložiště `nuget.org` , obnovení balíčků je zapnuto a balíčky se rozšiřují v `disk_drive_2/tmp` .</span><span class="sxs-lookup"><span data-stu-id="5fd30-180">As a result, the default repository on `nuget.org` is used, package restore is enabled, and packages get expanded in `disk_drive_2/tmp`.</span></span>

- <span data-ttu-id="5fd30-181">**Vyvoláno z `disk_drive_2/Project1` nebo `disk_drive_2/Project1/Source`**: nejprve se načte soubor na úrovni uživatele (a), pak NuGet načte soubor (B) z kořenové složky `disk_drive_2` a potom podle souboru (C).</span><span class="sxs-lookup"><span data-stu-id="5fd30-181">**Invoked from `disk_drive_2/Project1` or `disk_drive_2/Project1/Source`**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of `disk_drive_2`, followed by file (C).</span></span> <span data-ttu-id="5fd30-182">Nastavení v (C) přepíší ty v (B) a (A), takže `repositoryPath` balíčky WHERE se nainstalují, `disk_drive_2/Project1/External/Packages` místo `disk_drive_2/tmp` .</span><span class="sxs-lookup"><span data-stu-id="5fd30-182">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is `disk_drive_2/Project1/External/Packages` instead of `disk_drive_2/tmp`.</span></span> <span data-ttu-id="5fd30-183">V důsledku toho, že (C) vymazání `<packageSources>` , NuGet.org již není k dispozici jako zdroj opouští `https://MyPrivateRepo/ES/nuget` .</span><span class="sxs-lookup"><span data-stu-id="5fd30-183">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="5fd30-184">**Vyvoláno z `disk_drive_2/Project2` nebo `disk_drive_2/Project2/Source`**: nejprve se načte soubor na úrovni uživatele (a) následovaný souborem (B) a souborem (D).</span><span class="sxs-lookup"><span data-stu-id="5fd30-184">**Invoked from `disk_drive_2/Project2` or `disk_drive_2/Project2/Source`**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="5fd30-185">Vzhledem k tomu, že není `packageSources` zaškrtnuté, `nuget.org` a `https://MyPrivateRepo/DQ/nuget` jsou k dispozici jako zdroje.</span><span class="sxs-lookup"><span data-stu-id="5fd30-185">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="5fd30-186">Balíčky se rozšiřují v `disk_drive_2/tmp` , jak je uvedeno v (B).</span><span class="sxs-lookup"><span data-stu-id="5fd30-186">Packages get expanded in `disk_drive_2/tmp` as specified in (B).</span></span>

## <a name="additional-user-wide-configuration"></a><span data-ttu-id="5fd30-187">Další konfigurace pro nejrůznější uživatele</span><span class="sxs-lookup"><span data-stu-id="5fd30-187">Additional user wide configuration</span></span>

<span data-ttu-id="5fd30-188">Počínaje 5,7 se NuGet přidala podpora pro další konfigurační soubory, které jsou v uživatelském rozsahu.</span><span class="sxs-lookup"><span data-stu-id="5fd30-188">Starting with 5.7, NuGet has added support for additional user wide configuration files.</span></span> <span data-ttu-id="5fd30-189">To umožní dodavatelům třetích stran přidat další konfigurační soubory uživatele bez zvýšení oprávnění.</span><span class="sxs-lookup"><span data-stu-id="5fd30-189">This allows third-party vendors to add additional user configuration files without elevation.</span></span>
<span data-ttu-id="5fd30-190">Tyto konfigurační soubory se nacházejí ve složce standardní konfigurace pro všechny uživatele v `config` podsložce.</span><span class="sxs-lookup"><span data-stu-id="5fd30-190">These configuration files are found in the standard user wide configuration folder within a `config` subfolder.</span></span>
<span data-ttu-id="5fd30-191">Budou se brát v úvahu všechny soubory končící `.config` nebo `.Config` .</span><span class="sxs-lookup"><span data-stu-id="5fd30-191">All files ending with `.config` or `.Config` will be considered.</span></span>
<span data-ttu-id="5fd30-192">Tyto soubory nelze upravovat pomocí standardních nástrojů.</span><span class="sxs-lookup"><span data-stu-id="5fd30-192">These files cannot be edited by the standard tooling.</span></span>

| <span data-ttu-id="5fd30-193">Platforma operačního systému</span><span class="sxs-lookup"><span data-stu-id="5fd30-193">OS Platform</span></span>  | <span data-ttu-id="5fd30-194">Další konfigurace</span><span class="sxs-lookup"><span data-stu-id="5fd30-194">Additional Configurations</span></span> |
| --- | --- |
| <span data-ttu-id="5fd30-195">Windows</span><span class="sxs-lookup"><span data-stu-id="5fd30-195">Windows</span></span>      | `%appdata%\NuGet\config\*.Config` |
| <span data-ttu-id="5fd30-196">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="5fd30-196">Mac/Linux</span></span>    | <span data-ttu-id="5fd30-197">`~/.config/NuGet/config/*.config` nebo `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="5fd30-197">`~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> |

## <a name="nuget-defaults-file"></a><span data-ttu-id="5fd30-198">Soubor výchozích hodnot NuGet</span><span class="sxs-lookup"><span data-stu-id="5fd30-198">NuGet defaults file</span></span>

<span data-ttu-id="5fd30-199">`NuGetDefaults.Config`Soubor existuje za účelem určení zdrojů balíčků, ze kterých jsou balíčky nainstalovány a aktualizovány, a pro kontrolu výchozího cíle pro publikování balíčků pomocí `nuget push` .</span><span class="sxs-lookup"><span data-stu-id="5fd30-199">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="5fd30-200">Vzhledem k tomu, že správci můžou pohodlně (například pomocí Zásady skupiny) nasazovat konzistentní `NuGetDefaults.Config` soubory do počítačů pro vývojáře a sestavování, můžou zajistit, aby všichni v organizaci používali místo NuGet.org správné zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="5fd30-200">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="5fd30-201">`NuGetDefaults.Config`Soubor nikdy nezpůsobí odebrání zdroje balíčku z konfigurace NuGet vývojáře.</span><span class="sxs-lookup"><span data-stu-id="5fd30-201">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="5fd30-202">To znamená, že pokud vývojář již použil NuGet, a proto má registrovaný zdroj balíčku nuget.org, po vytvoření souboru se neodstraní `NuGetDefaults.Config` .</span><span class="sxs-lookup"><span data-stu-id="5fd30-202">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="5fd30-203">Navíc ani `NuGetDefaults.Config` žádný jiný mechanismus v NuGet nemůže zabránit přístupu ke zdrojům balíčků, jako je NuGet.org. Pokud si organizace chce takový přístup zablokovat, musí k tomu použít jiné prostředky, jako například brány firewall.</span><span class="sxs-lookup"><span data-stu-id="5fd30-203">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="5fd30-204">`NuGetDefaults.Config` oblasti</span><span class="sxs-lookup"><span data-stu-id="5fd30-204">`NuGetDefaults.Config` location</span></span>

<span data-ttu-id="5fd30-205">Následující tabulka popisuje `NuGetDefaults.Config` , kde by měl být soubor uložený v závislosti na cílovém operačním systému:</span><span class="sxs-lookup"><span data-stu-id="5fd30-205">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="5fd30-206">Platforma operačního systému</span><span class="sxs-lookup"><span data-stu-id="5fd30-206">OS Platform</span></span>  | <span data-ttu-id="5fd30-207">`NuGetDefaults.Config` Oblasti</span><span class="sxs-lookup"><span data-stu-id="5fd30-207">`NuGetDefaults.Config` Location</span></span> |
| --- | --- |
| <span data-ttu-id="5fd30-208">Windows</span><span class="sxs-lookup"><span data-stu-id="5fd30-208">Windows</span></span>      | <span data-ttu-id="5fd30-209">**Visual Studio 2017 nebo NuGet 4. x +:**`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="5fd30-209">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="5fd30-210">**Visual Studio 2015 a starší nebo NuGet 3. x a starší:**`%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="5fd30-210">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="5fd30-211">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="5fd30-211">Mac/Linux</span></span>    | <span data-ttu-id="5fd30-212">`$XDG_DATA_HOME` (obvykle `~/.local/share` nebo `/usr/local/share` , v závislosti na distribuci operačního systému)</span><span class="sxs-lookup"><span data-stu-id="5fd30-212">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="5fd30-213">Nastavení NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="5fd30-213">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="5fd30-214">`packageSources`: Tato kolekce má stejný význam jako `packageSources` v případě běžných konfiguračních souborů a určuje výchozí zdroje.</span><span class="sxs-lookup"><span data-stu-id="5fd30-214">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="5fd30-215">Nástroj NuGet používá zdroje v pořadí při instalaci nebo aktualizaci balíčků v projektech pomocí `packages.config` formátu správy.</span><span class="sxs-lookup"><span data-stu-id="5fd30-215">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="5fd30-216">Pro projekty, které používají formát PackageReference, NuGet používá nejprve místní zdroje, pak zdroje na sdílených síťových složkách a pak zdroje HTTP bez ohledu na pořadí v konfiguračních souborech.</span><span class="sxs-lookup"><span data-stu-id="5fd30-216">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="5fd30-217">NuGet vždycky ignoruje pořadí zdrojů s operacemi obnovení.</span><span class="sxs-lookup"><span data-stu-id="5fd30-217">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="5fd30-218">`disabledPackageSources`: Tato kolekce má také stejný význam jako v `NuGet.Config` souborech, kde je každý ovlivněný zdroj uveden podle názvu a hodnota, `true` / `false` která označuje, zda je zakázána.</span><span class="sxs-lookup"><span data-stu-id="5fd30-218">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a `true`/`false` value indicating whether it's disabled.</span></span> <span data-ttu-id="5fd30-219">Tím umožníte, aby název zdroje a adresa URL zůstaly v `packageSources` neaktivním stavu, aniž by bylo ve výchozím nastavení zapnuté.</span><span class="sxs-lookup"><span data-stu-id="5fd30-219">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="5fd30-220">Jednotliví vývojáři potom můžou zdroj znovu povolit nastavením hodnoty zdroje na `false` v jiných `NuGet.Config` souborech, aniž by museli znovu najít správnou adresu URL.</span><span class="sxs-lookup"><span data-stu-id="5fd30-220">Individual developers can then re-enable the source by setting the source's value to `false` in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="5fd30-221">To je užitečné také k tomu, aby vývojářům poskytoval úplný seznam interních zdrojových adres URL pro organizaci, přičemž ve výchozím nastavení povoluje pouze zdroj jednotlivých týmů.</span><span class="sxs-lookup"><span data-stu-id="5fd30-221">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="5fd30-222">`defaultPushSource`: Určuje výchozí cíl pro `nuget push` operace a přepíše vestavěnou výchozí hodnotu `nuget.org` .</span><span class="sxs-lookup"><span data-stu-id="5fd30-222">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of `nuget.org`.</span></span> <span data-ttu-id="5fd30-223">Správci můžou toto nastavení nasadit, aby nedocházelo k publikování interních balíčků `nuget.org` po havárii, protože vývojáři potřebují použít `nuget push -Source` k publikování na `nuget.org` .</span><span class="sxs-lookup"><span data-stu-id="5fd30-223">Administrators can deploy this setting to avoid publishing internal packages to the public `nuget.org` by accident, as developers specifically need to use `nuget push -Source` to publish to `nuget.org`.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="5fd30-224">Příklady NuGetDefaults.Config a aplikace</span><span class="sxs-lookup"><span data-stu-id="5fd30-224">Example NuGetDefaults.Config and application</span></span>

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
