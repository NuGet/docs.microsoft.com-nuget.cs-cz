---
title: "Příkaz zdroje NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: "Referenční dokumentace pro nuget.exe zdroje příkaz"
keywords: "nuget zdroje odkazu, zdroje příkaz"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2eca8557840c467a60f5f708efe242cd83609164
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/10/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="e198d-104">příkaz zdroje (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e198d-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="e198d-105">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="e198d-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="e198d-106">Spravuje seznam zdrojů, které jsou umístěné v `%AppData%\NuGet\NuGet.Config` nebo zadaný konfigurační soubor.</span><span class="sxs-lookup"><span data-stu-id="e198d-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

<span data-ttu-id="e198d-107">Všimněte si, že je adresa URL zdroje pro nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="e198d-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="e198d-108">Použití</span><span class="sxs-lookup"><span data-stu-id="e198d-108">Usage</span></span>

```
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="e198d-109">kde `<operation>` je jedním z *seznamu, přidat, odebrat, povolit, zakázat,* nebo *aktualizace*, `<name>` je název zdroje, a `<source>` je adresa URL zdroje.</span><span class="sxs-lookup"><span data-stu-id="e198d-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="e198d-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="e198d-110">Options</span></span>

| <span data-ttu-id="e198d-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="e198d-111">Option</span></span> | <span data-ttu-id="e198d-112">Popis</span><span class="sxs-lookup"><span data-stu-id="e198d-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e198d-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e198d-113">ConfigFile</span></span> | <span data-ttu-id="e198d-114">*(2.5 +)*  NuGet konfiguračním souboru použít.</span><span class="sxs-lookup"><span data-stu-id="e198d-114">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="e198d-115">Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá.</span><span class="sxs-lookup"><span data-stu-id="e198d-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="e198d-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e198d-116">ForceEnglishOutput</span></span> | <span data-ttu-id="e198d-117">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="e198d-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e198d-118">Formát</span><span class="sxs-lookup"><span data-stu-id="e198d-118">Format</span></span> | <span data-ttu-id="e198d-119">Platí pro `list` akce a může být `Detailed` (výchozí) nebo `Short`.</span><span class="sxs-lookup"><span data-stu-id="e198d-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="e198d-120">Nápověda</span><span class="sxs-lookup"><span data-stu-id="e198d-120">Help</span></span> | <span data-ttu-id="e198d-121">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="e198d-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="e198d-122">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="e198d-122">NonInteractive</span></span> | <span data-ttu-id="e198d-123">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="e198d-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e198d-124">Heslo</span><span class="sxs-lookup"><span data-stu-id="e198d-124">Password</span></span> | <span data-ttu-id="e198d-125">Určuje heslo pro ověřování se zdrojem.</span><span class="sxs-lookup"><span data-stu-id="e198d-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="e198d-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="e198d-126">StorePasswordInClearText</span></span> | <span data-ttu-id="e198d-127">Označuje uložit heslo v nezašifrované text namísto výchozího chování ukládání šifrovaném formátu.</span><span class="sxs-lookup"><span data-stu-id="e198d-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="e198d-128">UserName</span><span class="sxs-lookup"><span data-stu-id="e198d-128">UserName</span></span> | <span data-ttu-id="e198d-129">Určuje uživatelské jméno pro ověřování se zdrojem.</span><span class="sxs-lookup"><span data-stu-id="e198d-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="e198d-130">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="e198d-130">Verbosity</span></span> | <span data-ttu-id="e198d-131">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="e198d-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

> [!Note]
> <span data-ttu-id="e198d-132">Nezapomeňte přidat heslo u zdrojů ve stejném kontextu uživatele, jako nuget.exe se později používá pro přístup ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="e198d-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="e198d-133">Heslo se uloží zašifrované v konfiguračním souboru a mohou ho dešifrovat jenom v kontextu stejného uživatele jako byla zašifrovaná.</span><span class="sxs-lookup"><span data-stu-id="e198d-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="e198d-134">Takže například při použití sestavení serveru pro obnovení balíčků NuGet, které heslo musí být šifrovaný se stejným uživatelem systému Windows, ve kterém se spustí úlohu serveru sestavení.</span><span class="sxs-lookup"><span data-stu-id="e198d-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="e198d-135">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e198d-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e198d-136">Příklady</span><span class="sxs-lookup"><span data-stu-id="e198d-136">Examples</span></span>

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
