---
title: Zkontrolujte příkaz rozhraní příkazového řádku NuGet
description: Ověření odkazu nuget.exe příkaz
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545210"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="d53c2-103">Příkaz verify (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d53c2-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="d53c2-104">**Platí pro:** balíček spotřeby &bullet; **podporované verze:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="d53c2-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="d53c2-105">Ověří balíčku.</span><span class="sxs-lookup"><span data-stu-id="d53c2-105">Verifies a package.</span></span>

<span data-ttu-id="d53c2-106">V .NET Core, mono, nebo na platformách než Windows zatím nepodporuje ověření podepsaných balíčků.</span><span class="sxs-lookup"><span data-stu-id="d53c2-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="d53c2-107">Použití</span><span class="sxs-lookup"><span data-stu-id="d53c2-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="d53c2-108">kde `<package(s)>` je jeden nebo více `.nupkg` soubory.</span><span class="sxs-lookup"><span data-stu-id="d53c2-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="d53c2-109">ověřit nuget – vše</span><span class="sxs-lookup"><span data-stu-id="d53c2-109">nuget verify -All</span></span>

<span data-ttu-id="d53c2-110">Určuje, že všechny možné ověření je třeba provést na balíčky.</span><span class="sxs-lookup"><span data-stu-id="d53c2-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="d53c2-111">ověřování nuget - podpisů</span><span class="sxs-lookup"><span data-stu-id="d53c2-111">nuget verify -Signatures</span></span>

<span data-ttu-id="d53c2-112">Určuje, že by se měla provést ověření podpisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="d53c2-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="d53c2-113">Možnosti pro "ověřování - podpisů"</span><span class="sxs-lookup"><span data-stu-id="d53c2-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="d53c2-114">Možnost</span><span class="sxs-lookup"><span data-stu-id="d53c2-114">Option</span></span> | <span data-ttu-id="d53c2-115">Popis</span><span class="sxs-lookup"><span data-stu-id="d53c2-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d53c2-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="d53c2-116">CertificateFingerprint</span></span> | <span data-ttu-id="d53c2-117">Určuje jeden nebo více SHA-256 certifikát otisky prstů certifikátů (s), které podepsané balíčky musí být podepsán.</span><span class="sxs-lookup"><span data-stu-id="d53c2-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="d53c2-118">Otisk certifikátu SHA-256 se hashovací algoritmus SHA-256 certifikátu.</span><span class="sxs-lookup"><span data-stu-id="d53c2-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="d53c2-119">Více vstupů by měl být oddělený středníkem.</span><span class="sxs-lookup"><span data-stu-id="d53c2-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="d53c2-120">Možnosti</span><span class="sxs-lookup"><span data-stu-id="d53c2-120">Options</span></span>

| <span data-ttu-id="d53c2-121">Možnost</span><span class="sxs-lookup"><span data-stu-id="d53c2-121">Option</span></span> | <span data-ttu-id="d53c2-122">Popis</span><span class="sxs-lookup"><span data-stu-id="d53c2-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d53c2-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d53c2-123">ConfigFile</span></span> | <span data-ttu-id="d53c2-124">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="d53c2-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d53c2-125">Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="d53c2-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d53c2-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d53c2-126">ForceEnglishOutput</span></span> | <span data-ttu-id="d53c2-127">Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="d53c2-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d53c2-128">Nápověda</span><span class="sxs-lookup"><span data-stu-id="d53c2-128">Help</span></span> | <span data-ttu-id="d53c2-129">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="d53c2-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="d53c2-130">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="d53c2-130">Verbosity</span></span> | <span data-ttu-id="d53c2-131">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="d53c2-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="d53c2-132">Příklady</span><span class="sxs-lookup"><span data-stu-id="d53c2-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```