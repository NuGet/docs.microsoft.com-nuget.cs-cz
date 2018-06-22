---
title: Zkontrolujte příkaz NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro nuget.exe ověřte příkaz
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/23/2018
ms.locfileid: "34462849"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="14374-103">Příkaz verify (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="14374-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="14374-104">**Platí pro:** balíček spotřeba &bullet; **podporované verze:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="14374-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="14374-105">Ověřuje balíček.</span><span class="sxs-lookup"><span data-stu-id="14374-105">Verifies a package.</span></span>

<span data-ttu-id="14374-106">Ověření podepsaný balíčků v .NET Core, v části Mono nebo na jiný systém než Windows platformách ještě není podporovaný.</span><span class="sxs-lookup"><span data-stu-id="14374-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="14374-107">Použití</span><span class="sxs-lookup"><span data-stu-id="14374-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="14374-108">kde `<package(s)>` je jeden nebo více `.nupkg` soubory.</span><span class="sxs-lookup"><span data-stu-id="14374-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="14374-109">Ověřte nuget – všechny</span><span class="sxs-lookup"><span data-stu-id="14374-109">nuget verify -All</span></span>

<span data-ttu-id="14374-110">Určuje, že všechny možné ověření je třeba provést na balíčky.</span><span class="sxs-lookup"><span data-stu-id="14374-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="14374-111">ověřování nuget - podpisů</span><span class="sxs-lookup"><span data-stu-id="14374-111">nuget verify -Signatures</span></span>

<span data-ttu-id="14374-112">Určuje, že by se měla provést ověření podpisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="14374-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="14374-113">Možnosti pro "ověřit - podpisy"</span><span class="sxs-lookup"><span data-stu-id="14374-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="14374-114">Možnost</span><span class="sxs-lookup"><span data-stu-id="14374-114">Option</span></span> | <span data-ttu-id="14374-115">Popis</span><span class="sxs-lookup"><span data-stu-id="14374-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="14374-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="14374-116">CertificateFingerprint</span></span> | <span data-ttu-id="14374-117">Určuje jeden algoritmus SHA-256 certifikát otisky certifikátů (s), které podepsané balíčky musí být podepsány pomocí.</span><span class="sxs-lookup"><span data-stu-id="14374-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="14374-118">Otisk prstu certifikát SHA-256 je hodnota hash SHA-256 certifikátu.</span><span class="sxs-lookup"><span data-stu-id="14374-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="14374-119">Více vstupů by měl být oddělený středníkem.</span><span class="sxs-lookup"><span data-stu-id="14374-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="14374-120">Možnosti</span><span class="sxs-lookup"><span data-stu-id="14374-120">Options</span></span>

| <span data-ttu-id="14374-121">Možnost</span><span class="sxs-lookup"><span data-stu-id="14374-121">Option</span></span> | <span data-ttu-id="14374-122">Popis</span><span class="sxs-lookup"><span data-stu-id="14374-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="14374-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="14374-123">ConfigFile</span></span> | <span data-ttu-id="14374-124">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="14374-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="14374-125">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="14374-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="14374-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="14374-126">ForceEnglishOutput</span></span> | <span data-ttu-id="14374-127">Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="14374-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="14374-128">Nápověda</span><span class="sxs-lookup"><span data-stu-id="14374-128">Help</span></span> | <span data-ttu-id="14374-129">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="14374-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="14374-130">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="14374-130">Verbosity</span></span> | <span data-ttu-id="14374-131">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="14374-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="14374-132">Příklady</span><span class="sxs-lookup"><span data-stu-id="14374-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```