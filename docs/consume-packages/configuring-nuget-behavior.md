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
# <a name="configuring-nuget-behavior"></a><span data-ttu-id="1653c-103">Konfigurace chování Nugetu</span><span class="sxs-lookup"><span data-stu-id="1653c-103">Configuring NuGet behavior</span></span>

<span data-ttu-id="1653c-104">Chování Nugetu doprovází nahromaděné nastavení v jedné nebo více `NuGet.Config` soubory (XML), které mohou existovat úrovni projektu –, uživatel- a celý počítač.</span><span class="sxs-lookup"><span data-stu-id="1653c-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="1653c-105">Globální `NuGetDefaults.Config` soubor nastaví také konkrétně zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="1653c-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="1653c-106">Nastavení platí pro všechny příkazy vydané v rozhraní příkazového řádku, konzole Správce balíčků a uživatelské rozhraní Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="1653c-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="1653c-107">Umístění souboru konfigurace a použití</span><span class="sxs-lookup"><span data-stu-id="1653c-107">Config file locations and uses</span></span>

| <span data-ttu-id="1653c-108">Rozsah</span><span class="sxs-lookup"><span data-stu-id="1653c-108">Scope</span></span> | <span data-ttu-id="1653c-109">Umístění souboru NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="1653c-109">NuGet.Config file location</span></span> | <span data-ttu-id="1653c-110">Popis</span><span class="sxs-lookup"><span data-stu-id="1653c-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1653c-111">Projekt</span><span class="sxs-lookup"><span data-stu-id="1653c-111">Project</span></span> | <span data-ttu-id="1653c-112">Aktuální složce (označuje se také jako složka projektu) nebo libovolnou složku do kořenové jednotky.</span><span class="sxs-lookup"><span data-stu-id="1653c-112">Current folder (aka Project folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="1653c-113">Ve složce projektu nastavení platí jenom pro daný projekt.</span><span class="sxs-lookup"><span data-stu-id="1653c-113">In a project folder, settings apply only to that project.</span></span> <span data-ttu-id="1653c-114">V nadřazené složky, které obsahují více projektů podsložky nastavení platí pro všechny projekty v těchto podsložky.</span><span class="sxs-lookup"><span data-stu-id="1653c-114">In parent folders that contain multiple projects subfolders, settings apply to all projects in those subfolders.</span></span> |
| <span data-ttu-id="1653c-115">Uživatel</span><span class="sxs-lookup"><span data-stu-id="1653c-115">User</span></span> | <span data-ttu-id="1653c-116">Windows: `%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="1653c-116">Windows: `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="1653c-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` nebo `~/.nuget/NuGet/NuGet.Config` (se liší podle operačního systému distribučního)</span><span class="sxs-lookup"><span data-stu-id="1653c-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> | <span data-ttu-id="1653c-118">Nastavení platí pro všechny operace, ale jsou přepsány všechna nastavení na úrovni projektu.</span><span class="sxs-lookup"><span data-stu-id="1653c-118">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="1653c-119">Počítače</span><span class="sxs-lookup"><span data-stu-id="1653c-119">Computer</span></span> | <span data-ttu-id="1653c-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="1653c-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="1653c-121">Mac/Linux: `$XDG_DATA_HOME`.</span><span class="sxs-lookup"><span data-stu-id="1653c-121">Mac/Linux: `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="1653c-122">Pokud `$XDG_DATA_HOME` má hodnotu null nebo je prázdný, `~/.local/share` nebo `/usr/local/share` použije (se liší podle operačního systému distribučního)</span><span class="sxs-lookup"><span data-stu-id="1653c-122">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="1653c-123">Nastavení platí pro všechny operace v počítači, ale jsou přepsány žádné nastavení na úrovni uživatele nebo projektu.</span><span class="sxs-lookup"><span data-stu-id="1653c-123">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="1653c-124">Poznámky pro starší verze balíčku nuget:</span><span class="sxs-lookup"><span data-stu-id="1653c-124">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="1653c-125">NuGet 3.3 a dříve použitých `.nuget` složku pro nastavení řešení.</span><span class="sxs-lookup"><span data-stu-id="1653c-125">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="1653c-126">Tento soubor není používán ve Správci NuGet 3.4 +.</span><span class="sxs-lookup"><span data-stu-id="1653c-126">This file is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="1653c-127">NuGet 2.6 3.x, počítač úrovně konfiguračním souboru na Windows se nachází v % ProgramData%\NuGet\Config [\\{IDE} [\\{Version} [\\{SKU}]]]\NuGet.Config, kde *{IDE}* může být  *Visual Studio*, *{Version}* , jako je verze sady Visual Studio *14.0*, a *{SKU}* je buď *komunity*, *Pro*, nebo *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="1653c-127">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="1653c-128">Migrace nastavení na NuGet 4.0 +, jednoduše zkopírujte konfigurační soubor do % ProgramFiles(x86) % \NuGet\Config. V Linuxu, byl tento předchozí umístění /etc/opt a na Macu, Library/Application Support.</span><span class="sxs-lookup"><span data-stu-id="1653c-128">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="1653c-129">Změna nastavení konfigurace</span><span class="sxs-lookup"><span data-stu-id="1653c-129">Changing config settings</span></span>

<span data-ttu-id="1653c-130">A `NuGet.Config` souboru je jednoduchý textový soubor XML obsahující dvojice klíč/hodnota, jak je popsáno v [nastavení konfigurace NuGet](../reference/nuget-config-file.md) tématu.</span><span class="sxs-lookup"><span data-stu-id="1653c-130">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="1653c-131">Nastavení se spravují pomocí rozhraní příkazového řádku NuGet [příkaz config](../tools/cli-ref-config.md):</span><span class="sxs-lookup"><span data-stu-id="1653c-131">Settings are managed using the NuGet CLI [config command](../tools/cli-ref-config.md):</span></span>
- <span data-ttu-id="1653c-132">Ve výchozím nastavení jsou provedeny změny na úrovni uživatele konfiguračního souboru.</span><span class="sxs-lookup"><span data-stu-id="1653c-132">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="1653c-133">Chcete-li změnit nastavení v jiném souboru, použijte `-configFile` přepnout.</span><span class="sxs-lookup"><span data-stu-id="1653c-133">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="1653c-134">Soubory v tomto případě můžete použít libovolný název souboru.</span><span class="sxs-lookup"><span data-stu-id="1653c-134">In this case files can use any filename.</span></span>
- <span data-ttu-id="1653c-135">Klíče jsou vždy velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="1653c-135">Keys are always case sensitive.</span></span>
- <span data-ttu-id="1653c-136">Chcete-li změnit nastavení v souboru nastavení na úrovni počítače se vyžaduje zvýšení oprávnění.</span><span class="sxs-lookup"><span data-stu-id="1653c-136">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="1653c-137">I když můžete upravit soubor v libovolném textovém editoru, NuGet (v3.4.3 a novější) tiše ignoruje celý konfigurační soubor, pokud obsahuje nesprávně vytvořeným kódem XML (Neshoda značek, uvozovky neplatný atd.).</span><span class="sxs-lookup"><span data-stu-id="1653c-137">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="1653c-138">To je důvod, proč je vhodnější ke správě nastavení pomocí `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="1653c-138">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="1653c-139">Nastavení hodnoty</span><span class="sxs-lookup"><span data-stu-id="1653c-139">Setting a value</span></span>

<span data-ttu-id="1653c-140">Windows:</span><span class="sxs-lookup"><span data-stu-id="1653c-140">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="1653c-141">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="1653c-141">Mac/Linux:</span></span>

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
> <span data-ttu-id="1653c-142">NuGet 3.4 a vyšší můžete použít proměnné prostředí v libovolnou hodnotu, jako v `repositoryPath=%PACKAGEHOME%` (Windows) a `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="1653c-142">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="1653c-143">Odebrat hodnotu</span><span class="sxs-lookup"><span data-stu-id="1653c-143">Removing a value</span></span>

<span data-ttu-id="1653c-144">Pokud chcete odebrat hodnotu, zadejte klíč s prázdnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="1653c-144">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="1653c-145">Vytvoření nového souboru config</span><span class="sxs-lookup"><span data-stu-id="1653c-145">Creating a new config file</span></span>

<span data-ttu-id="1653c-146">Zkopírujte šablonu níže do nového souboru a pak použijte `nuget config -configFile <filename>` k nastavení hodnot:</span><span class="sxs-lookup"><span data-stu-id="1653c-146">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="1653c-147">Jak se používají nastavení</span><span class="sxs-lookup"><span data-stu-id="1653c-147">How settings are applied</span></span>

<span data-ttu-id="1653c-148">Více `NuGet.Config` soubory umožňují ukládat nastavení v různých umístěních, aby se vztahují na jednoho projektu, skupinu projektů nebo všechny projekty.</span><span class="sxs-lookup"><span data-stu-id="1653c-148">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="1653c-149">Tato nastavení se souhrnně platí pro všechny operace NuGet vyvolat z příkazového řádku nebo z aplikace Visual Studio s nastavením, které existují "nejbližší" do projektu nebo aktuální složce trvá prioritu.</span><span class="sxs-lookup"><span data-stu-id="1653c-149">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="1653c-150">Konkrétně NuGet načte nastavení z jiné konfigurační soubory v následujícím pořadí:</span><span class="sxs-lookup"><span data-stu-id="1653c-150">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="1653c-151">[NuGetDefaults.Config souboru](#nuget-defaults-file), který obsahuje nastavení související jenom s zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="1653c-151">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="1653c-152">Soubor úrovni počítače.</span><span class="sxs-lookup"><span data-stu-id="1653c-152">The computer-level file.</span></span>
1. <span data-ttu-id="1653c-153">Uživatelské úrovni souboru.</span><span class="sxs-lookup"><span data-stu-id="1653c-153">The user-level file.</span></span>
1. <span data-ttu-id="1653c-154">Soubor určený parametrem `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="1653c-154">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="1653c-155">Soubory nalezené v každé složky v cestě z kořenového adresáře disku do aktuální složky (Pokud je vyvolána nuget.exe nebo na složku obsahující projekt sady Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="1653c-155">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="1653c-156">Například, pokud příkaz je vyvolán v c:\A\B\C, NuGet vyhledá a načte konfigurační soubory v c:\, pak c:\A pak c:\A\B a nakonec c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="1653c-156">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="1653c-157">Jak NuGet najde nastavení v těchto souborech, použijí se následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="1653c-157">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="1653c-158">Pro prvky jedné položky NuGet nahradit libovolnou dříve najít hodnotu pro stejný klíč.</span><span class="sxs-lookup"><span data-stu-id="1653c-158">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="1653c-159">To znamená, že nastavení, které jsou "co nejblíž koncovým" aktuální složku nebo projekt přepsat všechny ostatní nalezen dříve.</span><span class="sxs-lookup"><span data-stu-id="1653c-159">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="1653c-160">Například `defaultPushSource` nastavení `NuGetDefaults.Config` je přepsána, pokud existuje v jiném konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="1653c-160">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="1653c-161">Kolekce elementů (například `<packageSources>`), NuGet kombinuje hodnoty z všechny konfigurační soubory do jedné kolekce.</span><span class="sxs-lookup"><span data-stu-id="1653c-161">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="1653c-162">Když `<clear />` je k dispozici pro daný uzel NuGet ignoruje dříve definovaným hodnotám konfigurace pro tento uzel.</span><span class="sxs-lookup"><span data-stu-id="1653c-162">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="1653c-163">Názorný postup nastavení</span><span class="sxs-lookup"><span data-stu-id="1653c-163">Settings walkthrough</span></span>

<span data-ttu-id="1653c-164">Řekněme, že mají následující strukturu složek na dvě samostatné jednotky:</span><span class="sxs-lookup"><span data-stu-id="1653c-164">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="1653c-165">Pak máte čtyři `NuGet.Config` soubory v následujících umístěních se daný obsah.</span><span class="sxs-lookup"><span data-stu-id="1653c-165">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="1653c-166">(Soubor úrovni počítače není zahrnuta v tomto příkladu, ale by se chovají podobně uživatelské úrovni souboru.)</span><span class="sxs-lookup"><span data-stu-id="1653c-166">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="1653c-167">Soubor individuální A. (`%appdata%\NuGet\NuGet.Config` na Windows, `~/.config/NuGet/NuGet.Config` na Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="1653c-167">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="1653c-168">Soubor B. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="1653c-168">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="1653c-169">Soubor C. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="1653c-169">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="1653c-170">Disk_drive_2/Project2/NuGet.Config D. souboru:</span><span class="sxs-lookup"><span data-stu-id="1653c-170">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="1653c-171">NuGet pak načte a použije nastavení následujícím způsobem, v závislosti na tom, kde je vyvolána:</span><span class="sxs-lookup"><span data-stu-id="1653c-171">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="1653c-172">**Vyvolat z disk_drive_1/uživatele v**: se používá pouze výchozí úložiště uvedené v souboru konfigurace na úrovni uživatele (A), protože se jedná o jediný soubor na disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="1653c-172">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="1653c-173">**Vyvolat z disk_drive_2 / nebo disk_drive_/tmp**: individuální souboru (A) je načten jako první, potom NuGet přejde do kořenového adresáře disk_drive_2 a najde soubor (B).</span><span class="sxs-lookup"><span data-stu-id="1653c-173">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="1653c-174">NuGet také hledá v konfiguračním souboru v TMP, ale nebyl nalezen jeden.</span><span class="sxs-lookup"><span data-stu-id="1653c-174">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="1653c-175">V důsledku toho se používá výchozí úložiště na nuget.org, obnovení balíčku je povolená a balíčky získat rozbalení v disk_drive_2/tmp.</span><span class="sxs-lookup"><span data-stu-id="1653c-175">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="1653c-176">**Vyvolání z disk_drive_2/Project1 nebo disk_drive_2/Project1/zdroje**: nejprve načtení souboru individuální (A) a pak NuGet načtení souboru (B) z kořenového adresáře disk_drive_2, za nímž následuje souboru (C).</span><span class="sxs-lookup"><span data-stu-id="1653c-176">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="1653c-177">Nastavení v (C) mají přednost před akcemi v (B) (A) a proto `repositoryPath` kde instalovat balíčky je disk_drive_2/Project1/externí/balíčky místo *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="1653c-177">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="1653c-178">Navíc protože (C) vymaže `<packageSources>`, nuget.org již není k dispozici jako zdroj byste museli opustit pouze `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="1653c-178">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="1653c-179">**Vyvolání z disk_drive_2 / "project2" nebo disk_drive_2 / "project2" / zdroje**: načtení souboru individuální (A) nejprve následovaný soubor (B) a soubor (D).</span><span class="sxs-lookup"><span data-stu-id="1653c-179">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="1653c-180">Protože `packageSources` není zaškrtnuto, obě `nuget.org` a `https://MyPrivateRepo/DQ/nuget` jsou k dispozici jako zdroje.</span><span class="sxs-lookup"><span data-stu-id="1653c-180">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="1653c-181">Získejte balíčky rozbalení v disk_drive_2/tmp, jak je uvedeno v (B).</span><span class="sxs-lookup"><span data-stu-id="1653c-181">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="1653c-182">Soubor výchozích hodnot NuGet</span><span class="sxs-lookup"><span data-stu-id="1653c-182">NuGet defaults file</span></span>

<span data-ttu-id="1653c-183">`NuGetDefaults.Config` Soubor existuje, můžete určit zdroje balíčků, ze kterých jsou nainstalované a aktualizovat balíčky a řídit výchozí cíl pro publikování balíčky s `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="1653c-183">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="1653c-184">Protože správci můžou jednoduše (například pomocí zásad skupiny) nasadit konzistentní `NuGetDefaults.Config` soubory na vývojáře a počítače sestavení, můžete zajistit, že všichni uživatelé v organizaci používá správný balíček zdroje místo nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1653c-184">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensuring that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="1653c-185">`NuGetDefaults.Config` Souboru nikdy způsobí, že zdroj balíčku, který chcete odebrat z konfigurace NuGet pro vývojáře.</span><span class="sxs-lookup"><span data-stu-id="1653c-185">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="1653c-186">To znamená, že pokud se už používá NuGet vývojář a proto má zdroj balíčku nuget.org zaregistrovali, se neodstraní po vytvoření `NuGetDefaults.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="1653c-186">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="1653c-187">Kromě toho, ani `NuGetDefaults.Config` ani jiný mechanismus ve Správci NuGet můžete zabránit přístupu k balíčku zdrojů, jako je nuget.org. Pokud organizace si přeje blokovat takový přístup, musí k tomu používat jiným způsobem, jako jsou brány firewall.</span><span class="sxs-lookup"><span data-stu-id="1653c-187">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="1653c-188">NuGetDefaults.Config umístění</span><span class="sxs-lookup"><span data-stu-id="1653c-188">NuGetDefaults.Config location</span></span>

<span data-ttu-id="1653c-189">Následující tabulka popisuje, kde `NuGetDefaults.Config` souboru by měla být uložena v závislosti na použitý operační systém:</span><span class="sxs-lookup"><span data-stu-id="1653c-189">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="1653c-190">Platforma operačního systému</span><span class="sxs-lookup"><span data-stu-id="1653c-190">OS Platform</span></span>  | <span data-ttu-id="1653c-191">NuGetDefaults.Config umístění</span><span class="sxs-lookup"><span data-stu-id="1653c-191">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="1653c-192">Windows</span><span class="sxs-lookup"><span data-stu-id="1653c-192">Windows</span></span>      | <span data-ttu-id="1653c-193">**Visual Studio 2017 nebo NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="1653c-193">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="1653c-194">**Visual Studio 2015 a starší nebo NuGet 3.x a dříve:** `%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="1653c-194">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="1653c-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="1653c-195">Mac/Linux</span></span>    | <span data-ttu-id="1653c-196">`$XDG_DATA_HOME` (obvykle `~/.local/share` nebo `/usr/local/share`, v závislosti na operačním systémem distribuce)</span><span class="sxs-lookup"><span data-stu-id="1653c-196">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="1653c-197">Nastavení NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="1653c-197">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="1653c-198">`packageSources`: Tato kolekce nemá stejný význam jako `packageSources` ve standardní konfigurační soubory a určí výchozí zdroje.</span><span class="sxs-lookup"><span data-stu-id="1653c-198">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="1653c-199">NuGet používá zdroje v pořadí při instalaci nebo aktualizaci balíčky v projektech pomocí `packages.config` formátu správy.</span><span class="sxs-lookup"><span data-stu-id="1653c-199">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="1653c-200">Pro projekty ve formátu PackageReference NuGet nejprve používá místní zdroje a pak zdrojů na sdílené síťové složky a zdrojů HTTP, bez ohledu na pořadí, v konfiguračních souborech.</span><span class="sxs-lookup"><span data-stu-id="1653c-200">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="1653c-201">NuGet vždy ignoruje pořadí zdrojů s operacemi obnovení.</span><span class="sxs-lookup"><span data-stu-id="1653c-201">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="1653c-202">`disabledPackageSources`: Tato kolekce má také stejný význam jako v `NuGet.Config` soubory, kde každý ovlivněné zdroj uvedené podle jeho název a hodnotu true nebo false určující, zda je zakázána.</span><span class="sxs-lookup"><span data-stu-id="1653c-202">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="1653c-203">To umožňuje název zdroje a adresa URL tak si zachováte `packageSources` bez nutnosti ho ve výchozím nastavení zapnutá.</span><span class="sxs-lookup"><span data-stu-id="1653c-203">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="1653c-204">Jednotliví vývojáři můžete potom znovu povolit zdroj podle zdroje na hodnotu nastavíte na hodnotu false v ostatních `NuGet.Config` soubory, aniž byste museli znovu najít správnou adresu URL.</span><span class="sxs-lookup"><span data-stu-id="1653c-204">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="1653c-205">To je užitečné k poskytování vývojářům úplný seznam adres URL vnitřního zdroje pro organizaci při povolování pouze zdroj jednotlivý tým ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="1653c-205">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="1653c-206">`defaultPushSource`: Určuje výchozí cíl pro `nuget push` operace, přepíšete integrovanou výchozí nuget.org. Správci můžou nasadit tohoto nastavení můžete zabránit publikování interní balíčků na nuget.org veřejné omylem, jak vývojáři konkrétně muset použít `nuget push -Source` publikovat na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1653c-206">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="1653c-207">Příklad NuGetDefaults.Config a aplikace</span><span class="sxs-lookup"><span data-stu-id="1653c-207">Example NuGetDefaults.Config and application</span></span>

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
