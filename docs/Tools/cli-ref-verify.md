---
title: Rozhraní příkazového řádku NuGet ověřte příkaz | Microsoft Docs
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro nuget.exe ověřte příkaz
keywords: ověření odkazu na nuget, ověřte příkaz
ms.reviewer:
- karann
- rmpablos
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4423e491e0ab5dc1e13982440db42bc9b0e85c38
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="0d621-104">Zkontrolujte příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0d621-104">verify command (NuGet CLI)</span></span>

<span data-ttu-id="0d621-105">**Platí pro:** balíček spotřeba &bullet; **podporované verze:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="0d621-105">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="0d621-106">Ověřuje balíček.</span><span class="sxs-lookup"><span data-stu-id="0d621-106">Verifies a package.</span></span>

## <a name="usage"></a><span data-ttu-id="0d621-107">Použití</span><span class="sxs-lookup"><span data-stu-id="0d621-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="0d621-108">kde `<package(s)>` je jeden nebo více `.nupkg` soubory.</span><span class="sxs-lookup"><span data-stu-id="0d621-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="0d621-109">Možnosti</span><span class="sxs-lookup"><span data-stu-id="0d621-109">Options</span></span>

| <span data-ttu-id="0d621-110">Možnost</span><span class="sxs-lookup"><span data-stu-id="0d621-110">Option</span></span> | <span data-ttu-id="0d621-111">Popis</span><span class="sxs-lookup"><span data-stu-id="0d621-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0d621-112">Všechny</span><span class="sxs-lookup"><span data-stu-id="0d621-112">All</span></span> | <span data-ttu-id="0d621-113">Určuje, že všechny možné ověření je třeba provést na balíčky.</span><span class="sxs-lookup"><span data-stu-id="0d621-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="0d621-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="0d621-114">CertificateFingerprint</span></span> | <span data-ttu-id="0d621-115">Určuje jeden algoritmus SHA-256 certifikát otisky certifikátů (s), které podepsané balíčky musí být podepsány pomocí.</span><span class="sxs-lookup"><span data-stu-id="0d621-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="0d621-116">Otisk prstu certifikát SHA-256 je hodnota hash SHA-256 certifikátu.</span><span class="sxs-lookup"><span data-stu-id="0d621-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="0d621-117">Více vstupů by měl být oddělený středníkem.</span><span class="sxs-lookup"><span data-stu-id="0d621-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="0d621-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0d621-118">ConfigFile</span></span> | <span data-ttu-id="0d621-119">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="0d621-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="0d621-120">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="0d621-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="0d621-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0d621-121">ForceEnglishOutput</span></span> | <span data-ttu-id="0d621-122">Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="0d621-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0d621-123">Nápověda</span><span class="sxs-lookup"><span data-stu-id="0d621-123">Help</span></span> | <span data-ttu-id="0d621-124">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="0d621-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="0d621-125">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="0d621-125">NonInteractive</span></span> | <span data-ttu-id="0d621-126">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="0d621-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0d621-127">Podpisy</span><span class="sxs-lookup"><span data-stu-id="0d621-127">Signatures</span></span> | <span data-ttu-id="0d621-128">Určuje, že by se měla provést ověření podpisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="0d621-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="0d621-129">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="0d621-129">Verbosity</span></span> | <span data-ttu-id="0d621-130">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="0d621-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="0d621-131">Příklady</span><span class="sxs-lookup"><span data-stu-id="0d621-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```