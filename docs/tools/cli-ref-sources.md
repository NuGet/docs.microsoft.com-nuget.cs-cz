---
title: Příkaz zdroje NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro nuget.exe zdroje příkaz
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d588ff09075ad75b76b7dd3645f3cdff29f6f093
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="de175-103">Příkaz sources (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="de175-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="de175-104">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="de175-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="de175-105">Spravuje seznam zdrojů, na které se nacházejí v oboru konfigurační soubor uživatele nebo v určeném konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="de175-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="de175-106">Konfigurační soubor uživatele rozsah se nachází v `%appdata%\NuGet\NuGet.Config` (Windows) a `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="de175-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="de175-107">Všimněte si, že je adresa URL zdroje pro nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="de175-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="de175-108">Použití</span><span class="sxs-lookup"><span data-stu-id="de175-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="de175-109">kde `<operation>` je jedním z *seznamu, přidat, odebrat, povolit, zakázat,* nebo *aktualizace*, `<name>` je název zdroje, a `<source>` je adresa URL zdroje.</span><span class="sxs-lookup"><span data-stu-id="de175-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="de175-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="de175-110">Options</span></span>

| <span data-ttu-id="de175-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="de175-111">Option</span></span> | <span data-ttu-id="de175-112">Popis</span><span class="sxs-lookup"><span data-stu-id="de175-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de175-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="de175-113">ConfigFile</span></span> | <span data-ttu-id="de175-114">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="de175-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="de175-115">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="de175-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="de175-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="de175-116">ForceEnglishOutput</span></span> | <span data-ttu-id="de175-117">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="de175-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="de175-118">Formát</span><span class="sxs-lookup"><span data-stu-id="de175-118">Format</span></span> | <span data-ttu-id="de175-119">Platí pro `list` akce a může být `Detailed` (výchozí) nebo `Short`.</span><span class="sxs-lookup"><span data-stu-id="de175-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="de175-120">Nápověda</span><span class="sxs-lookup"><span data-stu-id="de175-120">Help</span></span> | <span data-ttu-id="de175-121">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="de175-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="de175-122">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="de175-122">NonInteractive</span></span> | <span data-ttu-id="de175-123">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="de175-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="de175-124">Heslo</span><span class="sxs-lookup"><span data-stu-id="de175-124">Password</span></span> | <span data-ttu-id="de175-125">Určuje heslo pro ověřování se zdrojem.</span><span class="sxs-lookup"><span data-stu-id="de175-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="de175-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="de175-126">StorePasswordInClearText</span></span> | <span data-ttu-id="de175-127">Označuje uložit heslo v nezašifrované text namísto výchozího chování ukládání šifrovaném formátu.</span><span class="sxs-lookup"><span data-stu-id="de175-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="de175-128">UserName</span><span class="sxs-lookup"><span data-stu-id="de175-128">UserName</span></span> | <span data-ttu-id="de175-129">Určuje uživatelské jméno pro ověřování se zdrojem.</span><span class="sxs-lookup"><span data-stu-id="de175-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="de175-130">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="de175-130">Verbosity</span></span> | <span data-ttu-id="de175-131">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="de175-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="de175-132">Nezapomeňte přidat heslo u zdrojů ve stejném kontextu uživatele, jako nuget.exe se později používá pro přístup ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="de175-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="de175-133">Heslo se uloží zašifrované v konfiguračním souboru a mohou ho dešifrovat jenom v kontextu stejného uživatele jako byla zašifrovaná.</span><span class="sxs-lookup"><span data-stu-id="de175-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="de175-134">Takže například při použití sestavení serveru pro obnovení balíčků NuGet, které heslo musí být šifrovaný se stejným uživatelem systému Windows, ve kterém se spustí úlohu serveru sestavení.</span><span class="sxs-lookup"><span data-stu-id="de175-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="de175-135">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="de175-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="de175-136">Příklady</span><span class="sxs-lookup"><span data-stu-id="de175-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
