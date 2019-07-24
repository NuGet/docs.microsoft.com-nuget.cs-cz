---
title: NuGet CLI – příkaz ověření
description: Referenční informace o příkazu NuGet. exe Verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328252"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="e97b8-103">Příkaz verify (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e97b8-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="e97b8-104">**Platí pro:** &bullet; **podporované verze balíčku:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="e97b8-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="e97b8-105">Ověří balíček.</span><span class="sxs-lookup"><span data-stu-id="e97b8-105">Verifies a package.</span></span>

<span data-ttu-id="e97b8-106">Ověřování podepsaných balíčků se ještě nepodporuje v .NET Core, v mono nebo na platformách jiných než Windows.</span><span class="sxs-lookup"><span data-stu-id="e97b8-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="e97b8-107">Použití</span><span class="sxs-lookup"><span data-stu-id="e97b8-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="e97b8-108">kde `<package(s)>` je jeden nebo více `.nupkg` souborů.</span><span class="sxs-lookup"><span data-stu-id="e97b8-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="e97b8-109">NuGet ověřit – vše</span><span class="sxs-lookup"><span data-stu-id="e97b8-109">nuget verify -All</span></span>

<span data-ttu-id="e97b8-110">Určuje, že u balíčků by se měly provést všechna možná ověření.</span><span class="sxs-lookup"><span data-stu-id="e97b8-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="e97b8-111">ověření NuGet – signatury</span><span class="sxs-lookup"><span data-stu-id="e97b8-111">nuget verify -Signatures</span></span>

<span data-ttu-id="e97b8-112">Určuje, že by mělo být provedeno ověření podpisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="e97b8-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="e97b8-113">Možnosti pro "ověřit-podpisy"</span><span class="sxs-lookup"><span data-stu-id="e97b8-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="e97b8-114">Možnost</span><span class="sxs-lookup"><span data-stu-id="e97b8-114">Option</span></span> | <span data-ttu-id="e97b8-115">Popis</span><span class="sxs-lookup"><span data-stu-id="e97b8-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e97b8-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="e97b8-116">CertificateFingerprint</span></span> | <span data-ttu-id="e97b8-117">Určuje jeden nebo více otisků certifikátů SHA-256 certifikátů, které musí být podepsané balíčky podepsány.</span><span class="sxs-lookup"><span data-stu-id="e97b8-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="e97b8-118">Otisk certifikátu SHA-256 je hodnota hash SHA-256 certifikátu.</span><span class="sxs-lookup"><span data-stu-id="e97b8-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="e97b8-119">Více vstupů by mělo být odděleno středníkem.</span><span class="sxs-lookup"><span data-stu-id="e97b8-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="e97b8-120">Možnosti</span><span class="sxs-lookup"><span data-stu-id="e97b8-120">Options</span></span>

| <span data-ttu-id="e97b8-121">Možnost</span><span class="sxs-lookup"><span data-stu-id="e97b8-121">Option</span></span> | <span data-ttu-id="e97b8-122">Popis</span><span class="sxs-lookup"><span data-stu-id="e97b8-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e97b8-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e97b8-123">ConfigFile</span></span> | <span data-ttu-id="e97b8-124">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="e97b8-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e97b8-125">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="e97b8-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e97b8-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e97b8-126">ForceEnglishOutput</span></span> | <span data-ttu-id="e97b8-127">Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="e97b8-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e97b8-128">Help</span><span class="sxs-lookup"><span data-stu-id="e97b8-128">Help</span></span> | <span data-ttu-id="e97b8-129">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="e97b8-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="e97b8-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="e97b8-130">Verbosity</span></span> | <span data-ttu-id="e97b8-131">Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="e97b8-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="e97b8-132">Příklady</span><span class="sxs-lookup"><span data-stu-id="e97b8-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```