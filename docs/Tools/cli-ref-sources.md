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
ms.openlocfilehash: 52c46dba168e7395d50cb8d8f9775839389e614c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="d1c18-104">příkaz zdroje (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d1c18-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="d1c18-105">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="d1c18-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d1c18-106">Spravuje seznam zdrojů, které jsou umístěné v `%AppData%\NuGet\NuGet.Config` nebo zadaný konfigurační soubor.</span><span class="sxs-lookup"><span data-stu-id="d1c18-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

## <a name="usage"></a><span data-ttu-id="d1c18-107">Použití</span><span class="sxs-lookup"><span data-stu-id="d1c18-107">Usage</span></span>

```
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="d1c18-108">kde `<operation>` je jedním z *seznamu, přidat, odebrat, povolit, zakázat,* nebo *aktualizace*, `<name>` je název zdroje, a `<source>` je adresa URL zdroje.</span><span class="sxs-lookup"><span data-stu-id="d1c18-108">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>


## <a name="options"></a><span data-ttu-id="d1c18-109">Možnosti</span><span class="sxs-lookup"><span data-stu-id="d1c18-109">Options</span></span>

| <span data-ttu-id="d1c18-110">Možnost</span><span class="sxs-lookup"><span data-stu-id="d1c18-110">Option</span></span> | <span data-ttu-id="d1c18-111">Popis</span><span class="sxs-lookup"><span data-stu-id="d1c18-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1c18-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d1c18-112">ConfigFile</span></span> | <span data-ttu-id="d1c18-113">*(2.5 +)*  NuGet konfiguračním souboru použít.</span><span class="sxs-lookup"><span data-stu-id="d1c18-113">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="d1c18-114">Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá.</span><span class="sxs-lookup"><span data-stu-id="d1c18-114">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="d1c18-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d1c18-115">ForceEnglishOutput</span></span> | <span data-ttu-id="d1c18-116">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="d1c18-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d1c18-117">Formát</span><span class="sxs-lookup"><span data-stu-id="d1c18-117">Format</span></span> | <span data-ttu-id="d1c18-118">Platí pro `list` akce a může být `Detailed` (výchozí) nebo `Short`.</span><span class="sxs-lookup"><span data-stu-id="d1c18-118">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="d1c18-119">Nápověda</span><span class="sxs-lookup"><span data-stu-id="d1c18-119">Help</span></span> | <span data-ttu-id="d1c18-120">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="d1c18-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="d1c18-121">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="d1c18-121">NonInteractive</span></span> | <span data-ttu-id="d1c18-122">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="d1c18-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d1c18-123">Heslo</span><span class="sxs-lookup"><span data-stu-id="d1c18-123">Password</span></span> | <span data-ttu-id="d1c18-124">Určuje heslo pro ověřování se zdrojem.</span><span class="sxs-lookup"><span data-stu-id="d1c18-124">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="d1c18-125">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="d1c18-125">StorePasswordInClearText</span></span> | <span data-ttu-id="d1c18-126">Označuje uložit heslo v nezašifrované text namísto výchozího chování ukládání šifrovaném formátu.</span><span class="sxs-lookup"><span data-stu-id="d1c18-126">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="d1c18-127">UserName</span><span class="sxs-lookup"><span data-stu-id="d1c18-127">UserName</span></span> | <span data-ttu-id="d1c18-128">Určuje uživatelské jméno pro ověřování se zdrojem.</span><span class="sxs-lookup"><span data-stu-id="d1c18-128">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="d1c18-129">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="d1c18-129">Verbosity</span></span> | <span data-ttu-id="d1c18-130">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="d1c18-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

> [!Note]
> <span data-ttu-id="d1c18-131">Nezapomeňte přidat heslo u zdrojů ve stejném kontextu uživatele, jako nuget.exe se později používá pro přístup ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="d1c18-131">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="d1c18-132">Heslo se uloží zašifrované v konfiguračním souboru a mohou ho dešifrovat jenom v kontextu stejného uživatele jako byla zašifrovaná.</span><span class="sxs-lookup"><span data-stu-id="d1c18-132">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="d1c18-133">Takže například při použití sestavení serveru pro obnovení balíčků NuGet, které heslo musí být šifrovaný se stejným uživatelem systému Windows, ve kterém se spustí úlohu serveru sestavení.</span><span class="sxs-lookup"><span data-stu-id="d1c18-133">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="d1c18-134">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d1c18-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d1c18-135">Příklady</span><span class="sxs-lookup"><span data-stu-id="d1c18-135">Examples</span></span>

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
