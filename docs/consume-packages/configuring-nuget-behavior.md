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
# <a name="common-nuget-configurations"></a><span data-ttu-id="a421a-103">Běžné konfigurace NuGet</span><span class="sxs-lookup"><span data-stu-id="a421a-103">Common NuGet configurations</span></span>

<span data-ttu-id="a421a-104">Chování NuGet se řídí seshromážděným nastavením v jednom nebo několika souborech `NuGet.Config` (XML), které můžou existovat na úrovni projektu, uživatele a počítače.</span><span class="sxs-lookup"><span data-stu-id="a421a-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="a421a-105">Globální `NuGetDefaults.Config` soubor také konkrétně nakonfiguruje zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="a421a-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="a421a-106">Nastavení platí pro všechny příkazy vydávané v rozhraní příkazového řádku, konzole správce balíčků a uživatelské rozhraní Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="a421a-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="a421a-107">Umístění souborů konfigurace a použití</span><span class="sxs-lookup"><span data-stu-id="a421a-107">Config file locations and uses</span></span>

| <span data-ttu-id="a421a-108">Rozsah</span><span class="sxs-lookup"><span data-stu-id="a421a-108">Scope</span></span> | <span data-ttu-id="a421a-109">Umístění souboru NuGet. config</span><span class="sxs-lookup"><span data-stu-id="a421a-109">NuGet.Config file location</span></span> | <span data-ttu-id="a421a-110">Popis</span><span class="sxs-lookup"><span data-stu-id="a421a-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a421a-111">Řešení</span><span class="sxs-lookup"><span data-stu-id="a421a-111">Solution</span></span> | <span data-ttu-id="a421a-112">Aktuální složka (neboli složka řešení) nebo libovolná složka až do kořenového adresáře jednotky.</span><span class="sxs-lookup"><span data-stu-id="a421a-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="a421a-113">Ve složce řešení se nastavení aplikuje na všechny projekty v podsložkách.</span><span class="sxs-lookup"><span data-stu-id="a421a-113">In a solution folder, settings apply to all projects in subfolders.</span></span> <span data-ttu-id="a421a-114">Všimněte si, že pokud je konfigurační soubor umístěn ve složce projektu, nemá žádný vliv na tento projekt.</span><span class="sxs-lookup"><span data-stu-id="a421a-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="a421a-115">Uživatel</span><span class="sxs-lookup"><span data-stu-id="a421a-115">User</span></span> | <span data-ttu-id="a421a-116">Windows: `%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="a421a-116">Windows: `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="a421a-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` nebo `~/.nuget/NuGet/NuGet.Config` (liší se podle distribuce operačního systému)</span><span class="sxs-lookup"><span data-stu-id="a421a-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> | <span data-ttu-id="a421a-118">Nastavení platí pro všechny operace, ale jsou přepsána všemi nastaveními na úrovni projektu.</span><span class="sxs-lookup"><span data-stu-id="a421a-118">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="a421a-119">Počítač</span><span class="sxs-lookup"><span data-stu-id="a421a-119">Computer</span></span> | <span data-ttu-id="a421a-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="a421a-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="a421a-121">Mac/Linux: `$XDG_DATA_HOME`.</span><span class="sxs-lookup"><span data-stu-id="a421a-121">Mac/Linux: `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="a421a-122">Pokud `$XDG_DATA_HOME` má hodnotu null nebo je prázdné, bude použita `~/.local/share` nebo `/usr/local/share` (liší se podle distribuce operačního systému).</span><span class="sxs-lookup"><span data-stu-id="a421a-122">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="a421a-123">Nastavení platí pro všechny operace v počítači, ale jsou přepsána všemi uživateli nebo nastavením na úrovni projektu.</span><span class="sxs-lookup"><span data-stu-id="a421a-123">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="a421a-124">Poznámky pro starší verze NuGet:</span><span class="sxs-lookup"><span data-stu-id="a421a-124">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="a421a-125">NuGet 3,3 a starší používaly `.nuget` složku pro nastavení pro všechna řešení.</span><span class="sxs-lookup"><span data-stu-id="a421a-125">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="a421a-126">Tato složka se nepoužívá v NuGet 3.4 +.</span><span class="sxs-lookup"><span data-stu-id="a421a-126">This folder is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="a421a-127">Pro NuGet 2,6 až 3. x byl konfigurační soubor na úrovni počítače ve Windows umístěný v%ProgramData%\NuGet\Config [\\{IDE} [\\{Version} [\\{SKU}]]] \NuGet.Config, kde *{IDE}* může být *VisualStudio*, *{Version}* byla verze sady Visual Studio, jako je *14,0*a *{SKU}* je *komunita*, *pro*nebo *podnik*.</span><span class="sxs-lookup"><span data-stu-id="a421a-127">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="a421a-128">Chcete-li migrovat nastavení do NuGet 4.0 +, stačí zkopírovat konfigurační soubor do% ProgramFiles (x86)% \ NuGet\Config. V systému Linux se toto předchozí umístění/etc/opt a na Macu/Library/Application Support podpora.</span><span class="sxs-lookup"><span data-stu-id="a421a-128">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="a421a-129">Mění se nastavení konfigurace.</span><span class="sxs-lookup"><span data-stu-id="a421a-129">Changing config settings</span></span>

<span data-ttu-id="a421a-130">Soubor `NuGet.Config` je jednoduchý textový soubor XML obsahující páry klíč/hodnota, jak je popsáno v tématu [nastavení konfigurace NuGet](../reference/nuget-config-file.md) .</span><span class="sxs-lookup"><span data-stu-id="a421a-130">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="a421a-131">Nastavení se spravují pomocí příkazu NuGet CLI pro [konfiguraci](../reference/cli-reference/cli-ref-config.md):</span><span class="sxs-lookup"><span data-stu-id="a421a-131">Settings are managed using the NuGet CLI [config command](../reference/cli-reference/cli-ref-config.md):</span></span>
- <span data-ttu-id="a421a-132">Ve výchozím nastavení se změny provedou v konfiguračním souboru na úrovni uživatele.</span><span class="sxs-lookup"><span data-stu-id="a421a-132">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="a421a-133">Chcete-li změnit nastavení v jiném souboru, použijte přepínač `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="a421a-133">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="a421a-134">V tomto případě soubory můžou používat libovolný název souboru.</span><span class="sxs-lookup"><span data-stu-id="a421a-134">In this case files can use any filename.</span></span>
- <span data-ttu-id="a421a-135">U klíčů se rozlišují malá a velká písmena.</span><span class="sxs-lookup"><span data-stu-id="a421a-135">Keys are always case sensitive.</span></span>
- <span data-ttu-id="a421a-136">Ke změně nastavení v souboru nastavení na úrovni počítače je potřeba zvýšení oprávnění.</span><span class="sxs-lookup"><span data-stu-id="a421a-136">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="a421a-137">I když můžete soubor upravovat v libovolném textovém editoru, NuGet (v 3.4.3 a novějším) tiše ignoruje celý konfigurační soubor, pokud obsahuje nesprávně vytvořený kód XML (neshodné značky, neplatné uvozovky atd.).</span><span class="sxs-lookup"><span data-stu-id="a421a-137">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="a421a-138">To je důvod, proč je vhodnější spravovat nastavení pomocí `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="a421a-138">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="a421a-139">Nastavení hodnoty</span><span class="sxs-lookup"><span data-stu-id="a421a-139">Setting a value</span></span>

<span data-ttu-id="a421a-140">Windows:</span><span class="sxs-lookup"><span data-stu-id="a421a-140">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="a421a-141">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="a421a-141">Mac/Linux:</span></span>

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
> <span data-ttu-id="a421a-142">V NuGet 3,4 a novějších můžete použít proměnné prostředí v libovolné hodnotě, jako v `repositoryPath=%PACKAGEHOME%` (Windows) a `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="a421a-142">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="a421a-143">Odebrání hodnoty</span><span class="sxs-lookup"><span data-stu-id="a421a-143">Removing a value</span></span>

<span data-ttu-id="a421a-144">Chcete-li odebrat hodnotu, zadejte klíč s prázdnou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="a421a-144">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="a421a-145">Vytváření nového konfiguračního souboru</span><span class="sxs-lookup"><span data-stu-id="a421a-145">Creating a new config file</span></span>

<span data-ttu-id="a421a-146">Zkopírujte níže uvedenou šablonu do nového souboru a pak použijte `nuget config -configFile <filename>` k nastavení hodnot:</span><span class="sxs-lookup"><span data-stu-id="a421a-146">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="a421a-147">Způsob použití nastavení</span><span class="sxs-lookup"><span data-stu-id="a421a-147">How settings are applied</span></span>

<span data-ttu-id="a421a-148">Více `NuGet.Config` souborů vám umožní ukládat nastavení v různých umístěních, aby se mohla vztahovat na jeden projekt, skupinu projektů nebo všechny projekty.</span><span class="sxs-lookup"><span data-stu-id="a421a-148">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="a421a-149">Tato nastavení se souhrnně vztahují na jakoukoliv operaci NuGet vyvolanou z příkazového řádku nebo ze sady Visual Studio s nastaveními, která existují "nejblíže" do projektu, nebo když aktuální složka převezme přednost.</span><span class="sxs-lookup"><span data-stu-id="a421a-149">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="a421a-150">Konkrétně NuGet načte nastavení z různých konfiguračních souborů v následujícím pořadí:</span><span class="sxs-lookup"><span data-stu-id="a421a-150">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="a421a-151">[Soubor NuGetDefaults. config](#nuget-defaults-file)obsahující nastavení související pouze se zdroji balíčků.</span><span class="sxs-lookup"><span data-stu-id="a421a-151">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="a421a-152">Soubor na úrovni počítače.</span><span class="sxs-lookup"><span data-stu-id="a421a-152">The computer-level file.</span></span>
1. <span data-ttu-id="a421a-153">Soubor na úrovni uživatele.</span><span class="sxs-lookup"><span data-stu-id="a421a-153">The user-level file.</span></span>
1. <span data-ttu-id="a421a-154">Soubor zadaný pomocí `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="a421a-154">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="a421a-155">Soubory nalezené v každé složce v cestě z kořene jednotky do aktuální složky (kde je vyvolán NuGet. exe nebo složka obsahující projekt sady Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="a421a-155">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="a421a-156">Například pokud je příkaz vyvolán v c:\A\B\C, NuGet vyhledá a načte konfigurační soubory v jazyce c:\, potom c:\A, c:\A\B a finally c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="a421a-156">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="a421a-157">Jelikož NuGet najde nastavení těchto souborů, použije se takto:</span><span class="sxs-lookup"><span data-stu-id="a421a-157">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="a421a-158">Pro prvky s jednou položkou nahradila NuGet všechny dříve nalezené hodnoty pro stejný klíč.</span><span class="sxs-lookup"><span data-stu-id="a421a-158">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="a421a-159">To znamená, že nastavení, která jsou nejblíže aktuální složce nebo projektu, přepíší dříve nalezené.</span><span class="sxs-lookup"><span data-stu-id="a421a-159">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="a421a-160">Například nastavení `defaultPushSource` v `NuGetDefaults.Config` je přepsáno, pokud existuje v jiném konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="a421a-160">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="a421a-161">Pro prvky kolekce (například `<packageSources>`) NuGet kombinuje hodnoty ze všech konfiguračních souborů do jedné kolekce.</span><span class="sxs-lookup"><span data-stu-id="a421a-161">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="a421a-162">Pokud je pro daný uzel k dispozici `<clear />`, NuGet ignoruje dříve definované hodnoty konfigurace pro tento uzel.</span><span class="sxs-lookup"><span data-stu-id="a421a-162">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="a421a-163">Návod k nastavení</span><span class="sxs-lookup"><span data-stu-id="a421a-163">Settings walkthrough</span></span>

<span data-ttu-id="a421a-164">Řekněme, že máte na dvou samostatných jednotkách tuto strukturu složek:</span><span class="sxs-lookup"><span data-stu-id="a421a-164">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="a421a-165">Pak budete mít čtyři `NuGet.Config` soubory v následujících umístěních s daným obsahem.</span><span class="sxs-lookup"><span data-stu-id="a421a-165">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="a421a-166">(Soubor na úrovni počítače není v tomto příkladu zahrnutý, ale bude se chovat podobně jako soubor na úrovni uživatele.)</span><span class="sxs-lookup"><span data-stu-id="a421a-166">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="a421a-167">Soubor A. User-Level File (`%appdata%\NuGet\NuGet.Config` ve Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="a421a-167">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="a421a-168">Soubor B disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="a421a-168">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="a421a-169">Soubor C. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="a421a-169">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="a421a-170">Soubor D. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="a421a-170">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="a421a-171">NuGet potom načte a aplikuje nastavení podle toho, kde se vyvolalo:</span><span class="sxs-lookup"><span data-stu-id="a421a-171">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="a421a-172">**Vyvoláno z disk_drive_1/Users**: používá se jenom výchozí úložiště uvedené v konfiguračním souboru na úrovni uživatele (A), protože to je jediný soubor, který se nachází v disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="a421a-172">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="a421a-173">**Vyvoláno z disk_drive_2/nebo disk_drive_ adresáře/TMP**: nejprve se načte soubor na úrovni uživatele (a), pak NuGet přejde do kořenového adresáře disk_drive_2 a vyhledá soubor (B).</span><span class="sxs-lookup"><span data-stu-id="a421a-173">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="a421a-174">NuGet také hledá konfigurační soubor v adresáře/TMP, ale nenalezne ho.</span><span class="sxs-lookup"><span data-stu-id="a421a-174">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="a421a-175">V důsledku toho se použije výchozí úložiště v nuget.org, je povolené obnovení balíčků a balíčky se rozbalí v disk_drive_2/TMP.</span><span class="sxs-lookup"><span data-stu-id="a421a-175">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="a421a-176">**Vyvoláno z disk_drive_2/Project1 nebo disk_drive_2/Project1/source**: nejprve se načte soubor na úrovni uživatele (A), pak NuGet načte soubor (B) z kořenového adresáře disk_drive_2 následovaný souborem (C).</span><span class="sxs-lookup"><span data-stu-id="a421a-176">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="a421a-177">Nastavení v (C) přepíší ta v (B) a (A), takže `repositoryPath`, kde se balíčky nainstalují, disk_drive_2/Project1/External/Packages místo *disk_drive_2 adresáře/TMP*.</span><span class="sxs-lookup"><span data-stu-id="a421a-177">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="a421a-178">Z toho důvodu, že (C) vymaže `<packageSources>`nuget.org, již není k dispozici jako zdroj, který opouští pouze `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="a421a-178">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="a421a-179">**Vyvoláno z disk_drive_2/Project2 nebo disk_drive_2/Project2/source**: soubor na úrovni uživatele (A) se načte za prvé následovaný souborem (B) a souborem (D).</span><span class="sxs-lookup"><span data-stu-id="a421a-179">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="a421a-180">Vzhledem k tomu, že `packageSources` není zaškrtnuto, jsou jako zdroje k dispozici `nuget.org` a `https://MyPrivateRepo/DQ/nuget`.</span><span class="sxs-lookup"><span data-stu-id="a421a-180">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="a421a-181">Balíčky se rozšiřují v disk_drive_2 adresáře/TMP, jak je uvedeno v (B).</span><span class="sxs-lookup"><span data-stu-id="a421a-181">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="a421a-182">Soubor výchozích hodnot NuGet</span><span class="sxs-lookup"><span data-stu-id="a421a-182">NuGet defaults file</span></span>

<span data-ttu-id="a421a-183">`NuGetDefaults.Config` soubor existuje, chcete-li určit zdroje balíčků, ze kterých jsou balíčky nainstalovány a aktualizovány, a řídit výchozí cíl pro publikování balíčků pomocí `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="a421a-183">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="a421a-184">Vzhledem k tomu, že správci můžou pohodlně (například pomocí Zásady skupiny) nasazovat konzistentní `NuGetDefaults.Config` soubory pro vývojáře a sestavování počítačů, můžou zajistit, aby všichni v organizaci používali místo nuget.org správné zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="a421a-184">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="a421a-185">`NuGetDefaults.Config` soubor nikdy nezpůsobí odebrání zdroje balíčku z konfigurace NuGet vývojáře.</span><span class="sxs-lookup"><span data-stu-id="a421a-185">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="a421a-186">To znamená, že pokud vývojář již použil NuGet, a proto má registrovaný zdroj balíčku nuget.org, nebude po vytvoření souboru `NuGetDefaults.Config` odebrán.</span><span class="sxs-lookup"><span data-stu-id="a421a-186">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="a421a-187">Kromě toho ani `NuGetDefaults.Config` ani žádný jiný mechanismus v NuGet nemůže zabránit přístupu ke zdrojům balíčků, jako je nuget.org. Pokud si organizace chce takový přístup zablokovat, musí k tomu použít jiné prostředky, jako například brány firewall.</span><span class="sxs-lookup"><span data-stu-id="a421a-187">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="a421a-188">Umístění NuGetDefaults. config</span><span class="sxs-lookup"><span data-stu-id="a421a-188">NuGetDefaults.Config location</span></span>

<span data-ttu-id="a421a-189">Následující tabulka popisuje, kde by měl být soubor `NuGetDefaults.Config` uložený v závislosti na cílovém operačním systému:</span><span class="sxs-lookup"><span data-stu-id="a421a-189">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="a421a-190">Platforma operačního systému</span><span class="sxs-lookup"><span data-stu-id="a421a-190">OS Platform</span></span>  | <span data-ttu-id="a421a-191">Umístění NuGetDefaults. config</span><span class="sxs-lookup"><span data-stu-id="a421a-191">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="a421a-192">Windows</span><span class="sxs-lookup"><span data-stu-id="a421a-192">Windows</span></span>      | <span data-ttu-id="a421a-193">**Visual Studio 2017 nebo NuGet 4. x +:** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="a421a-193">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="a421a-194">**Visual Studio 2015 a starší nebo NuGet 3. x a starší:** `%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="a421a-194">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="a421a-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="a421a-195">Mac/Linux</span></span>    | <span data-ttu-id="a421a-196">`$XDG_DATA_HOME` (obvykle `~/.local/share` nebo `/usr/local/share`v závislosti na distribuci operačního systému)</span><span class="sxs-lookup"><span data-stu-id="a421a-196">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="a421a-197">Nastavení NuGetDefaults. config</span><span class="sxs-lookup"><span data-stu-id="a421a-197">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="a421a-198">`packageSources`: Tato kolekce má stejný význam jako `packageSources` v běžných konfiguračních souborech a určuje výchozí zdroje.</span><span class="sxs-lookup"><span data-stu-id="a421a-198">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="a421a-199">Nástroj NuGet používá zdroje v pořadí při instalaci nebo aktualizaci balíčků v projektech pomocí formátu správy `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="a421a-199">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="a421a-200">Pro projekty, které používají formát PackageReference, NuGet používá nejprve místní zdroje, pak zdroje na sdílených síťových složkách a pak zdroje HTTP bez ohledu na pořadí v konfiguračních souborech.</span><span class="sxs-lookup"><span data-stu-id="a421a-200">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="a421a-201">NuGet vždycky ignoruje pořadí zdrojů s operacemi obnovení.</span><span class="sxs-lookup"><span data-stu-id="a421a-201">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="a421a-202">`disabledPackageSources`: Tato kolekce má také stejný význam jako v souborech `NuGet.Config`, kde je každý ovlivněný zdroj uveden podle názvu a hodnota true/false, která označuje, jestli je zakázaná.</span><span class="sxs-lookup"><span data-stu-id="a421a-202">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="a421a-203">To umožňuje, aby název zdroje a adresa URL zůstaly v `packageSources`, aniž by bylo ve výchozím nastavení zapnuté.</span><span class="sxs-lookup"><span data-stu-id="a421a-203">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="a421a-204">Jednotliví vývojáři potom můžou zdroj znovu povolit nastavením hodnoty zdroje na hodnotu false v jiných `NuGet.Config` souborech, aniž by museli znovu najít správnou adresu URL.</span><span class="sxs-lookup"><span data-stu-id="a421a-204">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="a421a-205">To je užitečné také k tomu, aby vývojářům poskytoval úplný seznam interních zdrojových adres URL pro organizaci, přičemž ve výchozím nastavení povoluje pouze zdroj jednotlivých týmů.</span><span class="sxs-lookup"><span data-stu-id="a421a-205">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="a421a-206">`defaultPushSource`: Určuje výchozí cíl pro operace `nuget push` a přepíše vestavěnou výchozí hodnotu nuget.org. Správci můžou toto nastavení nasadit, aby nedocházelo k publikování interních balíčků na veřejném nuget.orgu po havárii, protože vývojáři potřebují k publikování do nuget.org použít `nuget push -Source`.</span><span class="sxs-lookup"><span data-stu-id="a421a-206">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="a421a-207">Příklad NuGetDefaults. config a Application</span><span class="sxs-lookup"><span data-stu-id="a421a-207">Example NuGetDefaults.Config and application</span></span>

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
