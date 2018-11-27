---
title: Rozhraní příkazového řádku NuGet důvěryhodné podepisující osoby
description: Referenční dokumentace pro důvěryhodného podepisující osoby příkaz nuget.exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ffd0cf5d50a2deed16e1722b32e43047bc81df2f
ms.sourcegitcommit: a1846edf70ddb2505d58e536e08e952d870931b0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/26/2018
ms.locfileid: "52303728"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="dda57-103">příkaz důvěryhodné podepisující osoby (rozhraní příkazového řádku NuGet)</span><span class="sxs-lookup"><span data-stu-id="dda57-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="dda57-104">**Platí pro:** balíček spotřeby &bullet; **podporované verze:** 4.9 +</span><span class="sxs-lookup"><span data-stu-id="dda57-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9+</span></span>

<span data-ttu-id="dda57-105">Získá nebo nastaví podepisující důvěryhodné osoby pro konfiguraci Nugetu.</span><span class="sxs-lookup"><span data-stu-id="dda57-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="dda57-106">Další využití, naleznete v tématu [konfigurace chování Nugetu](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="dda57-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="dda57-107">Podrobnosti o jak nuget.config schéma vypadá jako odkazovat [odkaz na soubor NuGet config](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="dda57-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="dda57-108">Použití</span><span class="sxs-lookup"><span data-stu-id="dda57-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="dda57-109">Pokud žádná z `list|add|remove|sync` není zadán, příkaz se ve výchozím nastavení `list`.</span><span class="sxs-lookup"><span data-stu-id="dda57-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="dda57-110">seznam důvěryhodných podepsaných nuget</span><span class="sxs-lookup"><span data-stu-id="dda57-110">nuget trusted-signers list</span></span>

<span data-ttu-id="dda57-111">Zobrazí seznam všech důvěryhodných podepsaných v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="dda57-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="dda57-112">Tato možnost zahrne všechny certifikáty (s otisku prstu a algoritmus otisk prstu) má každý podepisující osoba.</span><span class="sxs-lookup"><span data-stu-id="dda57-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="dda57-113">Pokud je certifikát předchozí `[U]`, znamená to, že položka certifikát má `allowUntrustedRoot` nastavit jako `true`.</span><span class="sxs-lookup"><span data-stu-id="dda57-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="dda57-114">Tady je příklad výstupu tohoto příkazu:</span><span class="sxs-lookup"><span data-stu-id="dda57-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="dda57-115">Přidat nuget důvěryhodné podepsaných [možnosti]</span><span class="sxs-lookup"><span data-stu-id="dda57-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="dda57-116">Přidá ke konfiguraci důvěryhodných podepisující osoba s daným názvem. Tuto možnost má jiné gesta můžete přidat důvěryhodného autora nebo úložiště.</span><span class="sxs-lookup"><span data-stu-id="dda57-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="dda57-117">Možnosti pro přidání závislosti na balíček</span><span class="sxs-lookup"><span data-stu-id="dda57-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="dda57-118">kde `<package(s)>` je jeden nebo více `.nupkg` soubory.</span><span class="sxs-lookup"><span data-stu-id="dda57-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="dda57-119">Možnost</span><span class="sxs-lookup"><span data-stu-id="dda57-119">Option</span></span> | <span data-ttu-id="dda57-120">Popis</span><span class="sxs-lookup"><span data-stu-id="dda57-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dda57-121">Autor</span><span class="sxs-lookup"><span data-stu-id="dda57-121">Author</span></span> | <span data-ttu-id="dda57-122">Určuje, že autor podpis balíčky, které by měl být důvěryhodný.</span><span class="sxs-lookup"><span data-stu-id="dda57-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="dda57-123">Úložiště</span><span class="sxs-lookup"><span data-stu-id="dda57-123">Repository</span></span> | <span data-ttu-id="dda57-124">Určuje, že podpis úložiště nebo potvrzovací podpis z balíčky musí být důvěryhodný.</span><span class="sxs-lookup"><span data-stu-id="dda57-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="dda57-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="dda57-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="dda57-126">Určuje, jestli certifikát pro důvěryhodného podepisující osoba by měla být povolená na řetězce na nedůvěryhodném kořenu.</span><span class="sxs-lookup"><span data-stu-id="dda57-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="dda57-127">Vlastníci</span><span class="sxs-lookup"><span data-stu-id="dda57-127">Owners</span></span> | <span data-ttu-id="dda57-128">Středníkem oddělený seznam vlastníků důvěryhodné pro další omezení důvěryhodnosti úložiště.</span><span class="sxs-lookup"><span data-stu-id="dda57-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="dda57-129">Platné jen v případě použití `-Repository` možnost.</span><span class="sxs-lookup"><span data-stu-id="dda57-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="dda57-130">Poskytuje i `-Author` a `-Repository` není podporováno ve stejnou dobu.</span><span class="sxs-lookup"><span data-stu-id="dda57-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="dda57-131">Možnosti pro přidání závislosti na index služby</span><span class="sxs-lookup"><span data-stu-id="dda57-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="dda57-132">_Poznámka:_: Tato možnost přidá jenom důvěryhodné úložiště.</span><span class="sxs-lookup"><span data-stu-id="dda57-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="dda57-133">Možnost</span><span class="sxs-lookup"><span data-stu-id="dda57-133">Option</span></span> | <span data-ttu-id="dda57-134">Popis</span><span class="sxs-lookup"><span data-stu-id="dda57-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dda57-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="dda57-135">ServiceIndex</span></span> | <span data-ttu-id="dda57-136">Určuje index služby V3 úložiště považovat za důvěryhodné.</span><span class="sxs-lookup"><span data-stu-id="dda57-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="dda57-137">Toto úložiště musí podporovat podpisy prostředků úložiště.</span><span class="sxs-lookup"><span data-stu-id="dda57-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="dda57-138">Pokud se nezadá, bude příkaz vypadat zdroje balíčku se stejným `-Name` a získat index služby z něj.</span><span class="sxs-lookup"><span data-stu-id="dda57-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="dda57-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="dda57-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="dda57-140">Určuje, jestli certifikát pro důvěryhodného podepisující osoba by měla být povolená na řetězce na nedůvěryhodném kořenu.</span><span class="sxs-lookup"><span data-stu-id="dda57-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="dda57-141">Vlastníci</span><span class="sxs-lookup"><span data-stu-id="dda57-141">Owners</span></span> | <span data-ttu-id="dda57-142">Středníkem oddělený seznam vlastníků důvěryhodné pro další omezení důvěryhodnosti úložiště.</span><span class="sxs-lookup"><span data-stu-id="dda57-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="dda57-143">Možnosti pro přidání na základě informací o certifikátu</span><span class="sxs-lookup"><span data-stu-id="dda57-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="dda57-144">_Poznámka:_: Pokud důvěryhodné podepisující osoba s daným názvem již existuje, položku certifikátu se přidají do této podepisující osoba.</span><span class="sxs-lookup"><span data-stu-id="dda57-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="dda57-145">V opačném případě důvěryhodného autora vytvoří s položkou certifikát z daných informace o certifikátu.</span><span class="sxs-lookup"><span data-stu-id="dda57-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="dda57-146">Možnost</span><span class="sxs-lookup"><span data-stu-id="dda57-146">Option</span></span> | <span data-ttu-id="dda57-147">Popis</span><span class="sxs-lookup"><span data-stu-id="dda57-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dda57-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="dda57-148">CertificateFingerprint</span></span> | <span data-ttu-id="dda57-149">Určuje certifikát, který musí být podepsáno otisky certifikátu, který podepsaných balíčků.</span><span class="sxs-lookup"><span data-stu-id="dda57-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="dda57-150">Otisk certifikátu je hodnota hash certifikátu.</span><span class="sxs-lookup"><span data-stu-id="dda57-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="dda57-151">Určuje algoritmus hash sloužící k výpočtu, tato hodnota hash by měla být v `FingerprintAlgorithm` možnost.</span><span class="sxs-lookup"><span data-stu-id="dda57-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="dda57-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="dda57-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="dda57-153">Určuje algoritmus hash používaný k výpočtu otisku certifikátu.</span><span class="sxs-lookup"><span data-stu-id="dda57-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="dda57-154">Výchozí hodnota je `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="dda57-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="dda57-155">Podporované hodnoty jsou `SHA256`, `SHA384` a `SHA512`</span><span class="sxs-lookup"><span data-stu-id="dda57-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="dda57-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="dda57-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="dda57-157">Určuje, jestli certifikát pro důvěryhodného podepisující osoba by měla být povolená na řetězce na nedůvěryhodném kořenu.</span><span class="sxs-lookup"><span data-stu-id="dda57-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="dda57-158">odebrat důvěryhodné nuget-podepsaných – název <name></span><span class="sxs-lookup"><span data-stu-id="dda57-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="dda57-159">Odebere všechny důvěryhodné podepisující osoby, které odpovídají zadaným názvem.</span><span class="sxs-lookup"><span data-stu-id="dda57-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="dda57-160">důvěryhodné nuget-podepsaných synchronizovat – název <name></span><span class="sxs-lookup"><span data-stu-id="dda57-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="dda57-161">Vyžaduje nejnovější seznam certifikátů používaných v současné době nedůvěryhodný úložiště aktualizovat seznamu existujících certifikátů v důvěryhodné podepisující osoba.</span><span class="sxs-lookup"><span data-stu-id="dda57-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="dda57-162">_Poznámka:_: Tento gesta odstraní aktuální seznam certifikátů a nahraďte aktuální seznam z úložiště.</span><span class="sxs-lookup"><span data-stu-id="dda57-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="dda57-163">Možnosti</span><span class="sxs-lookup"><span data-stu-id="dda57-163">Options</span></span>

| <span data-ttu-id="dda57-164">Možnost</span><span class="sxs-lookup"><span data-stu-id="dda57-164">Option</span></span> | <span data-ttu-id="dda57-165">Popis</span><span class="sxs-lookup"><span data-stu-id="dda57-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dda57-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="dda57-166">ConfigFile</span></span> | <span data-ttu-id="dda57-167">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="dda57-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="dda57-168">Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="dda57-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="dda57-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="dda57-169">ForceEnglishOutput</span></span> | <span data-ttu-id="dda57-170">Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="dda57-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="dda57-171">Nápověda</span><span class="sxs-lookup"><span data-stu-id="dda57-171">Help</span></span> | <span data-ttu-id="dda57-172">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="dda57-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="dda57-173">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="dda57-173">Verbosity</span></span> | <span data-ttu-id="dda57-174">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="dda57-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="dda57-175">Příklady</span><span class="sxs-lookup"><span data-stu-id="dda57-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```