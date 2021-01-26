---
title: NuGet CLI – příkaz konfigurace
description: Odkaz na příkaz nuget.exe config
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d50c12e34f71d7a62fe177da1dbb33eb702347a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775960"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="a68a7-103">příkaz config (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a68a7-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="a68a7-104">**Platí pro:** všechny &bullet; **podporované verze**: vše</span><span class="sxs-lookup"><span data-stu-id="a68a7-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="a68a7-105">Získá nebo nastaví hodnoty konfigurace NuGet.</span><span class="sxs-lookup"><span data-stu-id="a68a7-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="a68a7-106">Další informace o využití najdete v tématu [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="a68a7-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="a68a7-107">Podrobnosti o přípustných názvech klíčů najdete v odkazu na [konfigurační soubor NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="a68a7-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a68a7-108">Využití</span><span class="sxs-lookup"><span data-stu-id="a68a7-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="a68a7-109">kde `<name>` a `<value>` určuje dvojici klíč-hodnota, která má být nastavena v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="a68a7-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="a68a7-110">Můžete zadat libovolný počet párů podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="a68a7-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="a68a7-111">Chcete-li odebrat hodnotu, zadejte název a `=` znaménko, ale žádnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="a68a7-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="a68a7-112">Informace o přípustných klíčích klíčů najdete v referenční dokumentaci k [konfiguračnímu souboru NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="a68a7-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="a68a7-113">V NuGet 3.4 + `<value>` může použít [proměnné prostředí](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="a68a7-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="a68a7-114">Možnosti</span><span class="sxs-lookup"><span data-stu-id="a68a7-114">Options</span></span>


- **`AsPath`**

  <span data-ttu-id="a68a7-115">Vrátí hodnotu konfigurace jako cestu, při `-Set` použití se ignoruje.</span><span class="sxs-lookup"><span data-stu-id="a68a7-115">Returns the config value as a path, ignored when `-Set` is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a68a7-116">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="a68a7-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a68a7-117">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="a68a7-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a68a7-118">*(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="a68a7-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a68a7-119">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="a68a7-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a68a7-120">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="a68a7-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-Set`**

  <span data-ttu-id="a68a7-121">Jedna na další páry klíč-hodnota se nastaví v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="a68a7-121">One on more key-value pairs to be set in config.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a68a7-122">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="a68a7-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="a68a7-123">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="a68a7-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="a68a7-124">Příklady</span><span class="sxs-lookup"><span data-stu-id="a68a7-124">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
