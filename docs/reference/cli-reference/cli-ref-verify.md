---
title: NuGet CLI – příkaz ověření
description: Odkaz na příkaz nuget.exe Verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238137"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="af35c-103">VERIFY – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="af35c-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="af35c-104">**Platí pro:** &bullet; **podporované verze balíčku:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="af35c-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="af35c-105">Ověří balíček.</span><span class="sxs-lookup"><span data-stu-id="af35c-105">Verifies a package.</span></span>

<span data-ttu-id="af35c-106">Ověřování podepsaných balíčků ještě není v mono podporováno.</span><span class="sxs-lookup"><span data-stu-id="af35c-106">Verification of signed packages is not yet supported under Mono.</span></span>

## <a name="usage"></a><span data-ttu-id="af35c-107">Využití</span><span class="sxs-lookup"><span data-stu-id="af35c-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="af35c-108">kde `<package(s)>` je jeden nebo více `.nupkg` souborů.</span><span class="sxs-lookup"><span data-stu-id="af35c-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="af35c-109">NuGet ověřit – vše</span><span class="sxs-lookup"><span data-stu-id="af35c-109">nuget verify -All</span></span>

<span data-ttu-id="af35c-110">Určuje, že u balíčků by se měly provést všechna možná ověření.</span><span class="sxs-lookup"><span data-stu-id="af35c-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="af35c-111">ověření NuGet – signatury</span><span class="sxs-lookup"><span data-stu-id="af35c-111">nuget verify -Signatures</span></span>

<span data-ttu-id="af35c-112">Určuje, že by mělo být provedeno ověření podpisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="af35c-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="af35c-113">Možnosti pro "ověřit-podpisy"</span><span class="sxs-lookup"><span data-stu-id="af35c-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="af35c-114">Určuje jeden nebo více otisků certifikátů SHA-256 certifikátů, které musí být podepsané balíčky podepsány.</span><span class="sxs-lookup"><span data-stu-id="af35c-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="af35c-115">Otisk certifikátu SHA-256 je hodnota hash SHA-256 certifikátu.</span><span class="sxs-lookup"><span data-stu-id="af35c-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="af35c-116">Více vstupů by mělo být odděleno středníkem.</span><span class="sxs-lookup"><span data-stu-id="af35c-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="af35c-117">Možnosti</span><span class="sxs-lookup"><span data-stu-id="af35c-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="af35c-118">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="af35c-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="af35c-119">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="af35c-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="af35c-120">Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="af35c-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="af35c-121">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="af35c-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="af35c-122">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="af35c-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="af35c-123">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="af35c-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="af35c-124">Příklady</span><span class="sxs-lookup"><span data-stu-id="af35c-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```