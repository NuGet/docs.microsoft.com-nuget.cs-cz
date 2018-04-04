---
title: Příkaz zdroje NuGet rozhraní příkazového řádku | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro nuget.exe zdroje příkaz
keywords: nuget zdroje odkazu, zdroje příkaz
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5fb34654dc294de34cf0e15f784240884dc1e3d1
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/03/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="33dcc-104">příkaz zdroje (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="33dcc-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="33dcc-105">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="33dcc-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="33dcc-106">Spravuje seznam zdrojů, na které se nacházejí v oboru konfigurační soubor uživatele nebo v určeném konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="33dcc-106">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="33dcc-107">Konfigurační soubor uživatele rozsah se nachází v `%appdata%\NuGet\NuGet.Config` (Windows) a `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="33dcc-107">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="33dcc-108">Všimněte si, že je adresa URL zdroje pro nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="33dcc-108">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="33dcc-109">Použití</span><span class="sxs-lookup"><span data-stu-id="33dcc-109">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="33dcc-110">kde `<operation>` je jedním z *seznamu, přidat, odebrat, povolit, zakázat,* nebo *aktualizace*, `<name>` je název zdroje, a `<source>` je adresa URL zdroje.</span><span class="sxs-lookup"><span data-stu-id="33dcc-110">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="33dcc-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="33dcc-111">Options</span></span>

| <span data-ttu-id="33dcc-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="33dcc-112">Option</span></span> | <span data-ttu-id="33dcc-113">Popis</span><span class="sxs-lookup"><span data-stu-id="33dcc-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="33dcc-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="33dcc-114">ConfigFile</span></span> | <span data-ttu-id="33dcc-115">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="33dcc-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="33dcc-116">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="33dcc-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="33dcc-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="33dcc-117">ForceEnglishOutput</span></span> | <span data-ttu-id="33dcc-118">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="33dcc-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="33dcc-119">Formát</span><span class="sxs-lookup"><span data-stu-id="33dcc-119">Format</span></span> | <span data-ttu-id="33dcc-120">Platí pro `list` akce a může být `Detailed` (výchozí) nebo `Short`.</span><span class="sxs-lookup"><span data-stu-id="33dcc-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="33dcc-121">Nápověda</span><span class="sxs-lookup"><span data-stu-id="33dcc-121">Help</span></span> | <span data-ttu-id="33dcc-122">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="33dcc-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="33dcc-123">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="33dcc-123">NonInteractive</span></span> | <span data-ttu-id="33dcc-124">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="33dcc-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="33dcc-125">Heslo</span><span class="sxs-lookup"><span data-stu-id="33dcc-125">Password</span></span> | <span data-ttu-id="33dcc-126">Určuje heslo pro ověřování se zdrojem.</span><span class="sxs-lookup"><span data-stu-id="33dcc-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="33dcc-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="33dcc-127">StorePasswordInClearText</span></span> | <span data-ttu-id="33dcc-128">Označuje uložit heslo v nezašifrované text namísto výchozího chování ukládání šifrovaném formátu.</span><span class="sxs-lookup"><span data-stu-id="33dcc-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="33dcc-129">UserName</span><span class="sxs-lookup"><span data-stu-id="33dcc-129">UserName</span></span> | <span data-ttu-id="33dcc-130">Určuje uživatelské jméno pro ověřování se zdrojem.</span><span class="sxs-lookup"><span data-stu-id="33dcc-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="33dcc-131">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="33dcc-131">Verbosity</span></span> | <span data-ttu-id="33dcc-132">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="33dcc-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="33dcc-133">Nezapomeňte přidat heslo u zdrojů ve stejném kontextu uživatele, jako nuget.exe se později používá pro přístup ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="33dcc-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="33dcc-134">Heslo se uloží zašifrované v konfiguračním souboru a mohou ho dešifrovat jenom v kontextu stejného uživatele jako byla zašifrovaná.</span><span class="sxs-lookup"><span data-stu-id="33dcc-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="33dcc-135">Takže například při použití sestavení serveru pro obnovení balíčků NuGet, které heslo musí být šifrovaný se stejným uživatelem systému Windows, ve kterém se spustí úlohu serveru sestavení.</span><span class="sxs-lookup"><span data-stu-id="33dcc-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="33dcc-136">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="33dcc-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="33dcc-137">Příklady</span><span class="sxs-lookup"><span data-stu-id="33dcc-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
