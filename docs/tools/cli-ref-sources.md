---
title: Rozhraní příkazového řádku NuGet zdrojů příkaz
description: Odkaz nuget.exe zdrojů příkaz
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610619"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="97172-103">Příkaz sources (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="97172-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="97172-104">**Platí pro:** využití balíčků, publikováním &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="97172-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="97172-105">Spravuje seznam zdrojů nacházejí v oboru konfigurační soubor uživatele nebo zadaný konfigurační soubor.</span><span class="sxs-lookup"><span data-stu-id="97172-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="97172-106">Konfigurační soubor uživatele oboru se nachází v `%appdata%\NuGet\NuGet.Config` (Windows) a `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="97172-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="97172-107">Všimněte si, že je adresa URL zdroje pro nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="97172-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="97172-108">Použití</span><span class="sxs-lookup"><span data-stu-id="97172-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="97172-109">kde `<operation>` je jedním z *seznamu, přidávat, odstraňovat, povolit, zakázat,* nebo *aktualizace*, `<name>` je název zdroje, a `<source>` je zdrojové adrese URL.</span><span class="sxs-lookup"><span data-stu-id="97172-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="97172-110">Najednou můžete provozovat na jenom jeden zdroj.</span><span class="sxs-lookup"><span data-stu-id="97172-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="97172-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="97172-111">Options</span></span>

| <span data-ttu-id="97172-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="97172-112">Option</span></span> | <span data-ttu-id="97172-113">Popis</span><span class="sxs-lookup"><span data-stu-id="97172-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="97172-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="97172-114">ConfigFile</span></span> | <span data-ttu-id="97172-115">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="97172-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="97172-116">Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="97172-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="97172-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="97172-117">ForceEnglishOutput</span></span> | <span data-ttu-id="97172-118">*(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="97172-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="97172-119">Formát</span><span class="sxs-lookup"><span data-stu-id="97172-119">Format</span></span> | <span data-ttu-id="97172-120">Platí pro `list` akce a může být `Detailed` (výchozí) nebo `Short`.</span><span class="sxs-lookup"><span data-stu-id="97172-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="97172-121">Help</span><span class="sxs-lookup"><span data-stu-id="97172-121">Help</span></span> | <span data-ttu-id="97172-122">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="97172-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="97172-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="97172-123">NonInteractive</span></span> | <span data-ttu-id="97172-124">Potlačí vyzve k zadání uživatele o vstup ani potvrzení.</span><span class="sxs-lookup"><span data-stu-id="97172-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="97172-125">Heslo</span><span class="sxs-lookup"><span data-stu-id="97172-125">Password</span></span> | <span data-ttu-id="97172-126">Určuje heslo pro ověřování ve zdroji.</span><span class="sxs-lookup"><span data-stu-id="97172-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="97172-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="97172-127">StorePasswordInClearText</span></span> | <span data-ttu-id="97172-128">Označuje, že k uložení hesla v nešifrovaném textu místo výchozí chování ukládání zašifrované podobě.</span><span class="sxs-lookup"><span data-stu-id="97172-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="97172-129">UserName</span><span class="sxs-lookup"><span data-stu-id="97172-129">UserName</span></span> | <span data-ttu-id="97172-130">Určuje uživatelské jméno pro ověřování ve zdroji.</span><span class="sxs-lookup"><span data-stu-id="97172-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="97172-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="97172-131">Verbosity</span></span> | <span data-ttu-id="97172-132">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="97172-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="97172-133">Ujistěte se, že přidání hesla se zdroji ve stejném kontextu uživatele, protože nuget.exe se později používá pro přístup ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="97172-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="97172-134">Heslo bude uložen zašifrovaný v konfiguračním souboru a mohou ho dešifrovat jenom v rámci stejného uživatele jako byl zašifrován.</span><span class="sxs-lookup"><span data-stu-id="97172-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="97172-135">Proto například při použití serveru sestavení pro obnovování balíčků NuGet, které heslo musí být zašifrován pomocí stejného uživatele Windows, ve kterém se spustí úloha serveru sestavení.</span><span class="sxs-lookup"><span data-stu-id="97172-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="97172-136">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="97172-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="97172-137">Příklady</span><span class="sxs-lookup"><span data-stu-id="97172-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
