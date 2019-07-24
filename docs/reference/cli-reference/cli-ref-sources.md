---
title: NuGet – příkaz zdrojů CLI
description: Referenční informace o příkazu NuGet. exe sources
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328282"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="a99b5-103">Příkaz sources (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a99b5-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="a99b5-104">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzí:** vše</span><span class="sxs-lookup"><span data-stu-id="a99b5-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a99b5-105">Spravuje seznam zdrojů nacházejících se v konfiguračním souboru oboru uživatele nebo v zadaném konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="a99b5-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="a99b5-106">Konfigurační soubor oboru uživatele se nachází v `%appdata%\NuGet\NuGet.Config` (Windows) a `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="a99b5-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="a99b5-107">Všimněte si, že zdrojová adresa URL pro `https://api.nuget.org/v3/index.json`NuGet.org je.</span><span class="sxs-lookup"><span data-stu-id="a99b5-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="a99b5-108">Použití</span><span class="sxs-lookup"><span data-stu-id="a99b5-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="a99b5-109">kde `<operation>` je jedna z *seznamů, přidat, odebrat, povolit, zakázat* nebo *aktualizovat*, `<name>` je název zdroje a `<source>` je adresa URL zdroje.</span><span class="sxs-lookup"><span data-stu-id="a99b5-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="a99b5-110">V jednom okamžiku můžete pracovat jenom s jedním zdrojem.</span><span class="sxs-lookup"><span data-stu-id="a99b5-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="a99b5-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="a99b5-111">Options</span></span>

| <span data-ttu-id="a99b5-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="a99b5-112">Option</span></span> | <span data-ttu-id="a99b5-113">Popis</span><span class="sxs-lookup"><span data-stu-id="a99b5-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a99b5-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a99b5-114">ConfigFile</span></span> | <span data-ttu-id="a99b5-115">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="a99b5-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a99b5-116">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="a99b5-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a99b5-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a99b5-117">ForceEnglishOutput</span></span> | <span data-ttu-id="a99b5-118">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="a99b5-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a99b5-119">Formát</span><span class="sxs-lookup"><span data-stu-id="a99b5-119">Format</span></span> | <span data-ttu-id="a99b5-120">Platí pro `list` akci a může být `Detailed` (výchozí) nebo `Short`.</span><span class="sxs-lookup"><span data-stu-id="a99b5-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="a99b5-121">Help</span><span class="sxs-lookup"><span data-stu-id="a99b5-121">Help</span></span> | <span data-ttu-id="a99b5-122">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="a99b5-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="a99b5-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a99b5-123">NonInteractive</span></span> | <span data-ttu-id="a99b5-124">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="a99b5-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a99b5-125">Heslo</span><span class="sxs-lookup"><span data-stu-id="a99b5-125">Password</span></span> | <span data-ttu-id="a99b5-126">Určuje heslo pro ověřování ve zdroji.</span><span class="sxs-lookup"><span data-stu-id="a99b5-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="a99b5-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="a99b5-127">StorePasswordInClearText</span></span> | <span data-ttu-id="a99b5-128">Určuje, že se má uložit heslo v nešifrovaném textu namísto výchozího chování při ukládání šifrovaného formuláře.</span><span class="sxs-lookup"><span data-stu-id="a99b5-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="a99b5-129">UserName</span><span class="sxs-lookup"><span data-stu-id="a99b5-129">UserName</span></span> | <span data-ttu-id="a99b5-130">Určuje uživatelské jméno pro ověřování ve zdroji.</span><span class="sxs-lookup"><span data-stu-id="a99b5-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="a99b5-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="a99b5-131">Verbosity</span></span> | <span data-ttu-id="a99b5-132">Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="a99b5-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="a99b5-133">Nezapomeňte přidat "heslo zdrojů" v rámci stejného uživatelského kontextu, jako je soubor NuGet. exe, se později používá pro přístup ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="a99b5-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="a99b5-134">Heslo bude uloženo v konfiguračním souboru jako šifrované a lze ho dešifrovat pouze v kontextu stejného uživatele, který byl zašifrován.</span><span class="sxs-lookup"><span data-stu-id="a99b5-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="a99b5-135">Pokud například použijete sestavovací Server k obnovení balíčků NuGet, heslo musí být šifrované se stejným uživatelem systému Windows, pod kterým bude úloha sestavení serveru spuštěna.</span><span class="sxs-lookup"><span data-stu-id="a99b5-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="a99b5-136">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="a99b5-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a99b5-137">Příklady</span><span class="sxs-lookup"><span data-stu-id="a99b5-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
