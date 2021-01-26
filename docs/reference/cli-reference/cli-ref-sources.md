---
title: NuGet – příkaz zdrojů CLI
description: Referenční informace o příkazu nuget.exech zdrojů
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e9cbdd089c5c0f66d25e7588ece504feae63f2f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780004"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="20283-103">sources – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="20283-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="20283-104">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzí:** vše</span><span class="sxs-lookup"><span data-stu-id="20283-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="20283-105">Spravuje seznam zdrojů nacházejících se v konfiguračním souboru oboru uživatele nebo v zadaném konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="20283-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="20283-106">Konfigurační soubor oboru uživatele se nachází v `%appdata%\NuGet\NuGet.Config` (Windows) a `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="20283-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="20283-107">Všimněte si, že zdrojová adresa URL pro nuget.org je `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="20283-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="20283-108">Využití</span><span class="sxs-lookup"><span data-stu-id="20283-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="20283-109">kde `<operation>` je jedna z *seznamů, přidat, odebrat, povolit, zakázat* nebo *aktualizovat*, `<name>` je název zdroje a `<source>` je adresa URL zdroje.</span><span class="sxs-lookup"><span data-stu-id="20283-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="20283-110">V jednom okamžiku můžete pracovat jenom s jedním zdrojem.</span><span class="sxs-lookup"><span data-stu-id="20283-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="20283-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="20283-111">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="20283-112">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="20283-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="20283-113">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="20283-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="20283-114">*(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="20283-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Format`**

  <span data-ttu-id="20283-115">Platí pro `list` akci a může být `Detailed` (výchozí) nebo `Short` .</span><span class="sxs-lookup"><span data-stu-id="20283-115">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span>

- **`-?|-help`**

  <span data-ttu-id="20283-116">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="20283-116">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="20283-117">Název zdroje</span><span class="sxs-lookup"><span data-stu-id="20283-117">Name of the source.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="20283-118">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="20283-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Password`**

  <span data-ttu-id="20283-119">Určuje heslo pro ověřování ve zdroji.</span><span class="sxs-lookup"><span data-stu-id="20283-119">Specifies the password for authenticating with the source.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="20283-120">Cesta ke zdroji balíčku (ů)</span><span class="sxs-lookup"><span data-stu-id="20283-120">Path to the package(s) source.</span></span>

- **`-StorePasswordInClearText`**

  <span data-ttu-id="20283-121">Určuje, že se má uložit heslo v nešifrovaném textu namísto výchozího chování při ukládání šifrovaného formuláře.</span><span class="sxs-lookup"><span data-stu-id="20283-121">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span>

- **`-UserName`**

  <span data-ttu-id="20283-122">Určuje uživatelské jméno pro ověřování ve zdroji.</span><span class="sxs-lookup"><span data-stu-id="20283-122">Specifies the user name for authenticating with the source.</span></span>

- **`-ValidAuthenticationTypes`**

  <span data-ttu-id="20283-123">Čárkami oddělený seznam platných typů ověřování pro tento zdroj.</span><span class="sxs-lookup"><span data-stu-id="20283-123">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="20283-124">Ve výchozím nastavení jsou všechny typy ověřování platné.</span><span class="sxs-lookup"><span data-stu-id="20283-124">By default, all authentication types are valid.</span></span> <span data-ttu-id="20283-125">Příklad: `basic,negotiate`.</span><span class="sxs-lookup"><span data-stu-id="20283-125">Example: `basic,negotiate`.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="20283-126">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="20283-126">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

> [!Note]
> <span data-ttu-id="20283-127">Nezapomeňte přidat "heslo zdrojů" pod stejným uživatelským kontextem, protože nuget.exe se později používá pro přístup ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="20283-127">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="20283-128">Heslo bude uloženo v konfiguračním souboru jako šifrované a lze ho dešifrovat pouze v kontextu stejného uživatele, který byl zašifrován.</span><span class="sxs-lookup"><span data-stu-id="20283-128">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="20283-129">Pokud například použijete sestavovací Server k obnovení balíčků NuGet, heslo musí být šifrované se stejným uživatelem systému Windows, pod kterým bude úloha sestavení serveru spuštěna.</span><span class="sxs-lookup"><span data-stu-id="20283-129">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="20283-130">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="20283-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="20283-131">Příklady</span><span class="sxs-lookup"><span data-stu-id="20283-131">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
