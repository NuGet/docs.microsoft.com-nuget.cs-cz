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
# <a name="common-nuget-configurations"></a><span data-ttu-id="35b61-103">Běžné konfigurace NuGetu</span><span class="sxs-lookup"><span data-stu-id="35b61-103">Common NuGet configurations</span></span>

<span data-ttu-id="35b61-104">Chování nugetu je řízeno nahromaděnými nastaveními v jednom nebo více `NuGet.Config` (XML) souborech, které mohou existovat na úrovni celého projektu, uživatele a počítače.</span><span class="sxs-lookup"><span data-stu-id="35b61-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="35b61-105">Globální `NuGetDefaults.Config` soubor také konkrétně konfiguruje zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="35b61-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="35b61-106">Nastavení platí pro všechny příkazy vydané v příkazech příkazu příkazu cli, konzoly správce balíčků a ui Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="35b61-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="35b61-107">Umístění a použití konfiguračních souborů</span><span class="sxs-lookup"><span data-stu-id="35b61-107">Config file locations and uses</span></span>

| <span data-ttu-id="35b61-108">Rozsah</span><span class="sxs-lookup"><span data-stu-id="35b61-108">Scope</span></span> | <span data-ttu-id="35b61-109">Umístění souboru NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="35b61-109">NuGet.Config file location</span></span> | <span data-ttu-id="35b61-110">Popis</span><span class="sxs-lookup"><span data-stu-id="35b61-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="35b61-111">Řešení</span><span class="sxs-lookup"><span data-stu-id="35b61-111">Solution</span></span> | <span data-ttu-id="35b61-112">Aktuální složka (aka řešení složky) nebo libovolné složky až do kořenového adresáře jednotky.</span><span class="sxs-lookup"><span data-stu-id="35b61-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="35b61-113">Ve složce řešení platí nastavení pro všechny projekty v podsložkách.</span><span class="sxs-lookup"><span data-stu-id="35b61-113">In a solution folder, settings apply to all projects in subfolders.</span></span> <span data-ttu-id="35b61-114">Všimněte si, že pokud je konfigurační soubor umístěn do složky projektu, nemá na tento projekt žádný vliv.</span><span class="sxs-lookup"><span data-stu-id="35b61-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="35b61-115">Uživatel</span><span class="sxs-lookup"><span data-stu-id="35b61-115">User</span></span> | <span data-ttu-id="35b61-116">Windows:`%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="35b61-116">Windows: `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="35b61-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` `~/.nuget/NuGet/NuGet.Config` nebo (liší se podle distribuce operačního systému)</span><span class="sxs-lookup"><span data-stu-id="35b61-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> | <span data-ttu-id="35b61-118">Nastavení platí pro všechny operace, ale jsou přepsána všemi nastaveními na úrovni projektu.</span><span class="sxs-lookup"><span data-stu-id="35b61-118">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="35b61-119">Počítač</span><span class="sxs-lookup"><span data-stu-id="35b61-119">Computer</span></span> | <span data-ttu-id="35b61-120">Windows:`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="35b61-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="35b61-121">Mac/Linux: `$XDG_DATA_HOME`.</span><span class="sxs-lookup"><span data-stu-id="35b61-121">Mac/Linux: `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="35b61-122">Pokud `$XDG_DATA_HOME` je null `~/.local/share` nebo `/usr/local/share` prázdné, nebo budou použity (se liší podle distribuce operačního systému)</span><span class="sxs-lookup"><span data-stu-id="35b61-122">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="35b61-123">Nastavení platí pro všechny operace v počítači, ale jsou přepsána libovolným nastavením na úrovni uživatele nebo projektu.</span><span class="sxs-lookup"><span data-stu-id="35b61-123">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="35b61-124">Poznámky k dřívějším verzím nugetu:</span><span class="sxs-lookup"><span data-stu-id="35b61-124">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="35b61-125">NuGet 3.3 a `.nuget` starší používá složku pro nastavení celého řešení.</span><span class="sxs-lookup"><span data-stu-id="35b61-125">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="35b61-126">Tato složka se nepoužívá v NuGet 3.4+.</span><span class="sxs-lookup"><span data-stu-id="35b61-126">This folder is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="35b61-127">Pro soubor NuGet 2.6 až 3.x byl konfigurační soubor na úrovni počítače v\\systému Windows\\umístěn v\\%ProgramData%\NuGet\Config[ {IDE}[ {Version}[ {SKU}]]]\NuGet.Config, kde *{IDE}* může být *VisualStudio*, *{Version}* byla verze sady Visual Studio, například *14.0*, a *{SKU}* je *buď Community*, *Pro*, nebo *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="35b61-127">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="35b61-128">Chcete-li migrovat nastavení do položky NuGet 4.0+, jednoduše zkopírujte konfigurační soubor do %ProgramFiles(x86)%\NuGet\Config. Na Linuxu bylo toto předchozí umístění /etc/opt a na Macu, /Library/Application Support.</span><span class="sxs-lookup"><span data-stu-id="35b61-128">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="35b61-129">Změna nastavení konfigurace</span><span class="sxs-lookup"><span data-stu-id="35b61-129">Changing config settings</span></span>

<span data-ttu-id="35b61-130">Soubor `NuGet.Config` je jednoduchý textový soubor XML obsahující páry klíč/hodnota, jak je popsáno v tématu [Nastavení konfigurace NuGet.](../reference/nuget-config-file.md)</span><span class="sxs-lookup"><span data-stu-id="35b61-130">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="35b61-131">Nastavení jsou spravována pomocí [příkazu konfigurace příkazu](../reference/cli-reference/cli-ref-config.md)NuGet CLI :</span><span class="sxs-lookup"><span data-stu-id="35b61-131">Settings are managed using the NuGet CLI [config command](../reference/cli-reference/cli-ref-config.md):</span></span>
- <span data-ttu-id="35b61-132">Ve výchozím nastavení jsou změny v konfiguračním souboru na úrovni uživatele.</span><span class="sxs-lookup"><span data-stu-id="35b61-132">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="35b61-133">Chcete-li změnit nastavení v `-configFile` jiném souboru, použijte přepínač.</span><span class="sxs-lookup"><span data-stu-id="35b61-133">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="35b61-134">V tomto případě mohou soubory použít libovolný název souboru.</span><span class="sxs-lookup"><span data-stu-id="35b61-134">In this case files can use any filename.</span></span>
- <span data-ttu-id="35b61-135">Klíče jsou vždy rozlišována malá a velká písmena.</span><span class="sxs-lookup"><span data-stu-id="35b61-135">Keys are always case sensitive.</span></span>
- <span data-ttu-id="35b61-136">Zvýšení oprávnění je nutné ke změně nastavení v souboru nastavení na úrovni počítače.</span><span class="sxs-lookup"><span data-stu-id="35b61-136">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="35b61-137">Přestože můžete upravit soubor v libovolném textovém editoru, NuGet (v3.4.3 a novější) tiše ignoruje celý konfigurační soubor, pokud obsahuje poškozený XML (neodpovídající značky, neplatné uvozovky atd.).</span><span class="sxs-lookup"><span data-stu-id="35b61-137">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="35b61-138">To je důvod, proč je vhodnější `nuget config`spravovat nastavení pomocí .</span><span class="sxs-lookup"><span data-stu-id="35b61-138">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="35b61-139">Nastavení hodnoty</span><span class="sxs-lookup"><span data-stu-id="35b61-139">Setting a value</span></span>

<span data-ttu-id="35b61-140">Windows:</span><span class="sxs-lookup"><span data-stu-id="35b61-140">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="35b61-141">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="35b61-141">Mac/Linux:</span></span>

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
> <span data-ttu-id="35b61-142">V NuGet 3.4 a novější můžete použít proměnné prostředí `repositoryPath=%PACKAGEHOME%` v libovolné `repositoryPath=$PACKAGEHOME` hodnotě, jako v (Windows) a (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="35b61-142">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="35b61-143">Odebrání hodnoty</span><span class="sxs-lookup"><span data-stu-id="35b61-143">Removing a value</span></span>

<span data-ttu-id="35b61-144">Chcete-li odebrat hodnotu, zadejte klíč s prázdnou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="35b61-144">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="35b61-145">Vytvoření nového konfiguračního souboru</span><span class="sxs-lookup"><span data-stu-id="35b61-145">Creating a new config file</span></span>

<span data-ttu-id="35b61-146">Zkopírujte níže uvedenou šablonu `nuget config -configFile <filename>` do nového souboru a pak nastavte hodnoty:</span><span class="sxs-lookup"><span data-stu-id="35b61-146">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="35b61-147">Jak se nastavení používají</span><span class="sxs-lookup"><span data-stu-id="35b61-147">How settings are applied</span></span>

<span data-ttu-id="35b61-148">Více `NuGet.Config` souborů umožňuje ukládat nastavení v různých umístěních tak, aby se vztahovaly na jeden projekt, skupinu projektů nebo všechny projekty.</span><span class="sxs-lookup"><span data-stu-id="35b61-148">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="35b61-149">Tato nastavení společně platí pro všechny operace NuGet vyvolané z příkazového řádku nebo z Visual Studio, s nastavením, které existují "nejblíže" k projektu nebo aktuální složky s prioritou.</span><span class="sxs-lookup"><span data-stu-id="35b61-149">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="35b61-150">Konkrétně NuGet načte nastavení z různých konfiguračních souborů v následujícím pořadí:</span><span class="sxs-lookup"><span data-stu-id="35b61-150">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="35b61-151">[Soubor NuGetDefaults.Config](#nuget-defaults-file), který obsahuje nastavení související pouze se zdroji balíčků.</span><span class="sxs-lookup"><span data-stu-id="35b61-151">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="35b61-152">Soubor na úrovni počítače.</span><span class="sxs-lookup"><span data-stu-id="35b61-152">The computer-level file.</span></span>
1. <span data-ttu-id="35b61-153">Soubor na úrovni uživatele.</span><span class="sxs-lookup"><span data-stu-id="35b61-153">The user-level file.</span></span>
1. <span data-ttu-id="35b61-154">Soubor zadaný `-configFile`pomocí aplikace .</span><span class="sxs-lookup"><span data-stu-id="35b61-154">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="35b61-155">Soubory nalezené v každé složce v cestě od kořenového adresáře jednotky k aktuální složce (kde je vyvolán nuget.exe nebo složka obsahující projekt sady Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="35b61-155">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="35b61-156">Pokud je například příkaz vyvolán v c:\A\B\C, společnost NuGet vyhledá a\, načte konfigurační soubory do c: potom c:\A, potom c:\A\B a nakonec c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="35b61-156">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="35b61-157">Jako NuGet najde nastavení v těchto souborech, jsou použity takto:</span><span class="sxs-lookup"><span data-stu-id="35b61-157">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="35b61-158">Pro elementy s jednou položkou NuGet nahradil všechny dříve nalezené hodnoty pro stejný klíč.</span><span class="sxs-lookup"><span data-stu-id="35b61-158">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="35b61-159">To znamená, že nastavení, která jsou "nejblíže" k aktuální složce nebo projektu přepsat všechny ostatní našel dříve.</span><span class="sxs-lookup"><span data-stu-id="35b61-159">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="35b61-160">`defaultPushSource` Například nastavení in `NuGetDefaults.Config` je přepsáno, pokud existuje v jiném konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="35b61-160">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="35b61-161">Pro kolekce prvků `<packageSources>`(například ), NuGet kombinuje hodnoty ze všech konfiguračních souborů do jedné kolekce.</span><span class="sxs-lookup"><span data-stu-id="35b61-161">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="35b61-162">Pokud `<clear />` je k dispozici pro daný uzel, NuGet ignoruje dříve definované hodnoty konfigurace pro tento uzel.</span><span class="sxs-lookup"><span data-stu-id="35b61-162">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="35b61-163">Návod k nastavení</span><span class="sxs-lookup"><span data-stu-id="35b61-163">Settings walkthrough</span></span>

<span data-ttu-id="35b61-164">Řekněme, že máte následující strukturu složek na dvou samostatných jednotkách:</span><span class="sxs-lookup"><span data-stu-id="35b61-164">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="35b61-165">Potom máte `NuGet.Config` čtyři soubory v následujících umístěních s daným obsahem.</span><span class="sxs-lookup"><span data-stu-id="35b61-165">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="35b61-166">(Soubor na úrovni počítače není součástí tohoto příkladu, ale bude se chovat podobně jako soubor na úrovni uživatele.)</span><span class="sxs-lookup"><span data-stu-id="35b61-166">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="35b61-167">Soubor A. Soubor na`%appdata%\NuGet\NuGet.Config` úrovni uživatele, ( ve Windows, `~/.config/NuGet/NuGet.Config` na Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="35b61-167">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="35b61-168">Soubor B. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="35b61-168">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="35b61-169">Soubor C. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="35b61-169">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="35b61-170">Soubor D. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="35b61-170">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="35b61-171">NuGet pak načte a použije nastavení takto, v závislosti na tom, kde je vyvolána:</span><span class="sxs-lookup"><span data-stu-id="35b61-171">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="35b61-172">**Vyvoláno z disk_drive_1/uživatelů**: Používá se pouze výchozí úložiště uvedené v konfiguračním souboru na úrovni uživatele (A), protože je to jediný soubor nalezený na disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="35b61-172">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="35b61-173">**Vyvolána z disk_drive_2/ nebo disk_drive_/tmp**: Soubor na úrovni uživatele (A) je načten jako první, pak NuGet přejde do kořenového adresáře disk_drive_2 a najde soubor (B).</span><span class="sxs-lookup"><span data-stu-id="35b61-173">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="35b61-174">NuGet také hledá konfigurační soubor v /tmp, ale nenajde jeden.</span><span class="sxs-lookup"><span data-stu-id="35b61-174">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="35b61-175">V důsledku toho se používá výchozí úložiště na nuget.org, je povoleno obnovení balíčku a balíčky se rozbalí v disk_drive_2/tmp.</span><span class="sxs-lookup"><span data-stu-id="35b61-175">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="35b61-176">**Vyvolána z disk_drive_2/Project1 nebo disk_drive_2/Project1/Source**: Soubor na úrovni uživatele (A) je načten jako první, potom NuGet načte soubor (B) z kořenového adresáře disk_drive_2, následovaný souborem (C).</span><span class="sxs-lookup"><span data-stu-id="35b61-176">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="35b61-177">Nastavení v (C) přepsat ty v (B) `repositoryPath` a (A), takže kde se balíčky nainstalovat je disk_drive_2/Project1/External/Packages namísto *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="35b61-177">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="35b61-178">Také proto, že (C) vymaže `<packageSources>`, `https://MyPrivateRepo/ES/nuget`nuget.org již není k dispozici jako zdroj, který ponechá pouze .</span><span class="sxs-lookup"><span data-stu-id="35b61-178">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="35b61-179">**Vyvolána z disk_drive_2/Project2 nebo disk_drive_2/Project2/Source**: Soubor na úrovni uživatele (A) je načten nejprve následuje soubor (B) a soubor (D).</span><span class="sxs-lookup"><span data-stu-id="35b61-179">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="35b61-180">Protože `packageSources` není vymazána, `nuget.org` `https://MyPrivateRepo/DQ/nuget` oba a jsou k dispozici jako zdroje.</span><span class="sxs-lookup"><span data-stu-id="35b61-180">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="35b61-181">Balíčky se rozbalí v disk_drive_2/tmp, jak je uvedeno v (B).</span><span class="sxs-lookup"><span data-stu-id="35b61-181">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="35b61-182">NuGet výchozí soubor</span><span class="sxs-lookup"><span data-stu-id="35b61-182">NuGet defaults file</span></span>

<span data-ttu-id="35b61-183">Soubor `NuGetDefaults.Config` existuje, aby určil zdroje balíčků, ze kterých jsou balíčky nainstalovány `nuget push`a aktualizovány, a aby bylo nutné řídit výchozí cíl pro publikování balíčků pomocí aplikace .</span><span class="sxs-lookup"><span data-stu-id="35b61-183">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="35b61-184">Vzhledem k tomu, že správci mohou pohodlně `NuGetDefaults.Config` (například pomocí zásad skupiny) nasadit konzistentní soubory do vývojářských a buildových počítačů, mohou zajistit, aby všichni v organizaci používali správné zdroje balíčků, nikoli nuget.org.</span><span class="sxs-lookup"><span data-stu-id="35b61-184">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="35b61-185">Soubor `NuGetDefaults.Config` nikdy způsobí, že zdroj balíčku, které mají být odebrány z konfigurace nuget vývojáře.</span><span class="sxs-lookup"><span data-stu-id="35b61-185">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="35b61-186">To znamená, že pokud vývojář již použil NuGet a proto má nuget.org zdroj balíčku `NuGetDefaults.Config` registrován, nebude odebrán po vytvoření souboru.</span><span class="sxs-lookup"><span data-stu-id="35b61-186">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="35b61-187">Kromě toho ani `NuGetDefaults.Config` žádný jiný mechanismus v NuGet můžete zabránit přístupu ke zdrojům balíčku, jako je nuget.org. Pokud organizace chce blokovat takový přístup, musí k tomu použít jiné prostředky, například brány firewall.</span><span class="sxs-lookup"><span data-stu-id="35b61-187">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="35b61-188">Umístění NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="35b61-188">NuGetDefaults.Config location</span></span>

<span data-ttu-id="35b61-189">Následující tabulka popisuje, `NuGetDefaults.Config` kde by měl být soubor uložen v závislosti na cílovém os:</span><span class="sxs-lookup"><span data-stu-id="35b61-189">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="35b61-190">Platforma Operačního eS</span><span class="sxs-lookup"><span data-stu-id="35b61-190">OS Platform</span></span>  | <span data-ttu-id="35b61-191">Umístění NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="35b61-191">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="35b61-192">Windows</span><span class="sxs-lookup"><span data-stu-id="35b61-192">Windows</span></span>      | <span data-ttu-id="35b61-193">**Visual Studio 2017 nebo NuGet 4.x+:**`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="35b61-193">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="35b61-194">**Visual Studio 2015 a starší nebo NuGet 3.x a starší:**`%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="35b61-194">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="35b61-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="35b61-195">Mac/Linux</span></span>    | <span data-ttu-id="35b61-196">`$XDG_DATA_HOME`(obvykle `~/.local/share` nebo `/usr/local/share`, v závislosti na distribuci Operačního systému)</span><span class="sxs-lookup"><span data-stu-id="35b61-196">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="35b61-197">Nastavení NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="35b61-197">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="35b61-198">`packageSources`: Tato kolekce má `packageSources` stejný význam jako v běžných konfiguračních souborech a určuje výchozí zdroje.</span><span class="sxs-lookup"><span data-stu-id="35b61-198">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="35b61-199">NuGet používá zdroje v pořadí při instalaci nebo `packages.config` aktualizaci balíčků v projektech pomocí formátu pro správu.</span><span class="sxs-lookup"><span data-stu-id="35b61-199">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="35b61-200">Pro projekty používající formát PackageReference nuget nejprve používá místní zdroje, pak zdroje na sdílené síťové složky, pak zdroje HTTP, bez ohledu na pořadí v konfiguračních souborech.</span><span class="sxs-lookup"><span data-stu-id="35b61-200">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="35b61-201">NuGet vždy ignoruje pořadí zdrojů s operaceobnovení.</span><span class="sxs-lookup"><span data-stu-id="35b61-201">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="35b61-202">`disabledPackageSources`: Tato kolekce má také `NuGet.Config` stejný význam jako v souborech, kde každý ohrožený zdroj je uveden podle jeho názvu a true/false hodnotu označující, zda je zakázán.</span><span class="sxs-lookup"><span data-stu-id="35b61-202">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="35b61-203">To umožňuje, aby zdrojový název `packageSources` a adresa URL zůstaly ve výchozím nastavení, aniž by byly zapnuty.</span><span class="sxs-lookup"><span data-stu-id="35b61-203">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="35b61-204">Jednotliví vývojáři pak mohou znovu povolit zdroj nastavením `NuGet.Config` hodnoty zdroje na false v jiných souborech, aniž by museli znovu najít správnou adresu URL.</span><span class="sxs-lookup"><span data-stu-id="35b61-204">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="35b61-205">To je také užitečné pro poskytování vývojářům úplný seznam interních zdrojových adres URL pro organizaci a zároveň ve výchozím nastavení povolit pouze zdroj jednotlivých týmů.</span><span class="sxs-lookup"><span data-stu-id="35b61-205">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="35b61-206">`defaultPushSource`: určuje výchozí cíl `nuget push` pro operace, přepsání předdefinované výchozí nuget.org. Správci mohou toto nastavení nasadit, aby se zabránilo publikování interních `nuget push -Source` balíčků na veřejné nuget.org náhodou, protože vývojáři konkrétně potřebují publikovat do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="35b61-206">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="35b61-207">Příklad NuGetDefaults.Config a aplikace</span><span class="sxs-lookup"><span data-stu-id="35b61-207">Example NuGetDefaults.Config and application</span></span>

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
