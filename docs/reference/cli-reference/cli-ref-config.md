---
title: NuGet CLI – příkaz konfigurace
description: Referenční informace k příkazu NuGet. exe config
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433319"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="a0693-103">příkaz config (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a0693-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="a0693-104">**Platí pro:** všechny &bullet; **podporované verze**: vše</span><span class="sxs-lookup"><span data-stu-id="a0693-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="a0693-105">Získá nebo nastaví hodnoty konfigurace NuGet.</span><span class="sxs-lookup"><span data-stu-id="a0693-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="a0693-106">Další informace o využití najdete v tématu [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="a0693-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="a0693-107">Podrobnosti o přípustných názvech klíčů najdete v odkazu na [konfigurační soubor NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="a0693-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a0693-108">Použití</span><span class="sxs-lookup"><span data-stu-id="a0693-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="a0693-109">kde `<name>` a`<value>` určuje dvojici klíč-hodnota, která má být nastavena v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="a0693-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="a0693-110">Můžete zadat libovolný počet párů podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="a0693-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="a0693-111">Chcete-li odebrat hodnotu, zadejte název a `=` znaménko, ale žádnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="a0693-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="a0693-112">Informace o přípustných klíčích klíčů najdete v referenční dokumentaci k [konfiguračnímu souboru NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="a0693-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="a0693-113">V NuGet 3.4 + `<value>` může použít [proměnné prostředí](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="a0693-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="a0693-114">Možnosti</span><span class="sxs-lookup"><span data-stu-id="a0693-114">Options</span></span>

| <span data-ttu-id="a0693-115">Možnost</span><span class="sxs-lookup"><span data-stu-id="a0693-115">Option</span></span> | <span data-ttu-id="a0693-116">Popis</span><span class="sxs-lookup"><span data-stu-id="a0693-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a0693-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="a0693-117">AsPath</span></span> | <span data-ttu-id="a0693-118">Vrátí hodnotu konfigurace jako cestu, při `-Set` použití se ignoruje.</span><span class="sxs-lookup"><span data-stu-id="a0693-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="a0693-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a0693-119">ConfigFile</span></span> | <span data-ttu-id="a0693-120">Konfigurační soubor NuGet, který se má upravit.</span><span class="sxs-lookup"><span data-stu-id="a0693-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="a0693-121">Pokud tento parametr nezadáte, použije se výchozí soubor`%AppData%\NuGet\NuGet.Config` – (Windows) `~/.config/NuGet/NuGet.Config` nebo (Mac/Linux) `~/.nuget/NuGet/NuGet.Config` nebo (závisí na distribuci OS).</span><span class="sxs-lookup"><span data-stu-id="a0693-121">If not specified, the default file is used -`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.config/NuGet/NuGet.Config`  (Mac/Linux) or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution).</span></span>|
| <span data-ttu-id="a0693-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a0693-122">ForceEnglishOutput</span></span> | <span data-ttu-id="a0693-123">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="a0693-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a0693-124">Help</span><span class="sxs-lookup"><span data-stu-id="a0693-124">Help</span></span> | <span data-ttu-id="a0693-125">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="a0693-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="a0693-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a0693-126">NonInteractive</span></span> | <span data-ttu-id="a0693-127">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="a0693-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a0693-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="a0693-128">Verbosity</span></span> | <span data-ttu-id="a0693-129">Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="a0693-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a0693-130">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="a0693-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="a0693-131">Příklady</span><span class="sxs-lookup"><span data-stu-id="a0693-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
