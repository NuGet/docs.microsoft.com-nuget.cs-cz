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
ms.openlocfilehash: f682a5209556ec6741473ccf2648e8f38bb568b9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="dac67-104">příkaz zdroje (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="dac67-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="dac67-105">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="dac67-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="dac67-106">Spravuje seznam zdrojů, na které se nacházejí v oboru konfigurační soubor uživatele nebo v určeném konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="dac67-106">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="dac67-107">Konfigurační soubor uživatele rozsah se nachází v `%appdata%\NuGet\NuGet.Config` (Windows) a `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="dac67-107">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="dac67-108">Všimněte si, že je adresa URL zdroje pro nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="dac67-108">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="dac67-109">Použití</span><span class="sxs-lookup"><span data-stu-id="dac67-109">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="dac67-110">kde `<operation>` je jedním z *seznamu, přidat, odebrat, povolit, zakázat,* nebo *aktualizace*, `<name>` je název zdroje, a `<source>` je adresa URL zdroje.</span><span class="sxs-lookup"><span data-stu-id="dac67-110">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="dac67-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="dac67-111">Options</span></span>

| <span data-ttu-id="dac67-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="dac67-112">Option</span></span> | <span data-ttu-id="dac67-113">Popis</span><span class="sxs-lookup"><span data-stu-id="dac67-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dac67-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="dac67-114">ConfigFile</span></span> | <span data-ttu-id="dac67-115">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="dac67-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="dac67-116">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="dac67-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="dac67-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="dac67-117">ForceEnglishOutput</span></span> | <span data-ttu-id="dac67-118">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="dac67-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="dac67-119">Formát</span><span class="sxs-lookup"><span data-stu-id="dac67-119">Format</span></span> | <span data-ttu-id="dac67-120">Platí pro `list` akce a může být `Detailed` (výchozí) nebo `Short`.</span><span class="sxs-lookup"><span data-stu-id="dac67-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="dac67-121">Nápověda</span><span class="sxs-lookup"><span data-stu-id="dac67-121">Help</span></span> | <span data-ttu-id="dac67-122">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="dac67-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="dac67-123">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="dac67-123">NonInteractive</span></span> | <span data-ttu-id="dac67-124">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="dac67-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="dac67-125">Heslo</span><span class="sxs-lookup"><span data-stu-id="dac67-125">Password</span></span> | <span data-ttu-id="dac67-126">Určuje heslo pro ověřování se zdrojem.</span><span class="sxs-lookup"><span data-stu-id="dac67-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="dac67-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="dac67-127">StorePasswordInClearText</span></span> | <span data-ttu-id="dac67-128">Označuje uložit heslo v nezašifrované text namísto výchozího chování ukládání šifrovaném formátu.</span><span class="sxs-lookup"><span data-stu-id="dac67-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="dac67-129">UserName</span><span class="sxs-lookup"><span data-stu-id="dac67-129">UserName</span></span> | <span data-ttu-id="dac67-130">Určuje uživatelské jméno pro ověřování se zdrojem.</span><span class="sxs-lookup"><span data-stu-id="dac67-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="dac67-131">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="dac67-131">Verbosity</span></span> | <span data-ttu-id="dac67-132">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="dac67-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="dac67-133">Nezapomeňte přidat heslo u zdrojů ve stejném kontextu uživatele, jako nuget.exe se později používá pro přístup ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="dac67-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="dac67-134">Heslo se uloží zašifrované v konfiguračním souboru a mohou ho dešifrovat jenom v kontextu stejného uživatele jako byla zašifrovaná.</span><span class="sxs-lookup"><span data-stu-id="dac67-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="dac67-135">Takže například při použití sestavení serveru pro obnovení balíčků NuGet, které heslo musí být šifrovaný se stejným uživatelem systému Windows, ve kterém se spustí úlohu serveru sestavení.</span><span class="sxs-lookup"><span data-stu-id="dac67-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="dac67-136">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="dac67-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="dac67-137">Příklady</span><span class="sxs-lookup"><span data-stu-id="dac67-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
