---
title: Příkaz NuGet CLI Trusted-signers
description: Referenční informace k příkazu NuGet. exe Trusted-signers
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 94c4c6524c1870898893b80be914477af5a14e8b
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610337"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="f167b-103">příkaz důvěryhodného přihlášení (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f167b-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="f167b-104">**Platí pro:** spotřeba balíčku &bullet; **podporované verze:** 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="f167b-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="f167b-105">Získá nebo nastaví důvěryhodné podepisující osoby na konfiguraci NuGet.</span><span class="sxs-lookup"><span data-stu-id="f167b-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="f167b-106">Další informace o využití najdete v tématu [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="f167b-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="f167b-107">Podrobnosti o tom, jak vypadá schéma NuGet. config, najdete v odkazu na [konfigurační soubor NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="f167b-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="f167b-108">Použití</span><span class="sxs-lookup"><span data-stu-id="f167b-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="f167b-109">Pokud není zadán žádný z `list|add|remove|sync`, bude příkaz ve výchozím nastavení `list`.</span><span class="sxs-lookup"><span data-stu-id="f167b-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="f167b-110">seznam důvěryhodných podpisů NuGet</span><span class="sxs-lookup"><span data-stu-id="f167b-110">nuget trusted-signers list</span></span>

<span data-ttu-id="f167b-111">Zobrazí seznam všech důvěryhodných přihlášení v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="f167b-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="f167b-112">Tato možnost zahrne všechny certifikáty (s otiskem prstu a otiskem prstu) každého podepsaného.</span><span class="sxs-lookup"><span data-stu-id="f167b-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="f167b-113">Pokud certifikát obsahuje předchozí `[U]`, znamená to, že položka certifikátu má `allowUntrustedRoot` nastavená jako `true`.</span><span class="sxs-lookup"><span data-stu-id="f167b-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="f167b-114">Níže je uvedený příklad výstupu z tohoto příkazu:</span><span class="sxs-lookup"><span data-stu-id="f167b-114">Below is an example output from this command:</span></span>

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

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="f167b-115">Důvěryhodní přihlášení NuGet – přidat [možnosti]</span><span class="sxs-lookup"><span data-stu-id="f167b-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="f167b-116">Přidá důvěryhodného podepisujícího se zadaným názvem do konfiguračního souboru. Tato možnost obsahuje různá gesta pro přidání důvěryhodného autora nebo úložiště.</span><span class="sxs-lookup"><span data-stu-id="f167b-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="f167b-117">Možnosti pro přidání na základě balíčku</span><span class="sxs-lookup"><span data-stu-id="f167b-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="f167b-118">kde `<package(s)>` je jeden nebo více `.nupkg` souborů.</span><span class="sxs-lookup"><span data-stu-id="f167b-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="f167b-119">Možnost</span><span class="sxs-lookup"><span data-stu-id="f167b-119">Option</span></span> | <span data-ttu-id="f167b-120">Popis</span><span class="sxs-lookup"><span data-stu-id="f167b-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f167b-121">Autorizova</span><span class="sxs-lookup"><span data-stu-id="f167b-121">Author</span></span> | <span data-ttu-id="f167b-122">Určuje, že podpis autora balíčků by měl být důvěryhodný.</span><span class="sxs-lookup"><span data-stu-id="f167b-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="f167b-123">Úložištì</span><span class="sxs-lookup"><span data-stu-id="f167b-123">Repository</span></span> | <span data-ttu-id="f167b-124">Určuje, že signatura úložiště nebo potvrzovací podpisy balíčků by měly být důvěryhodné.</span><span class="sxs-lookup"><span data-stu-id="f167b-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="f167b-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="f167b-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="f167b-126">Určuje, jestli by měl být certifikát pro důvěryhodného podepisujícího povolený řetězení k nedůvěryhodnému kořenovému adresáři.</span><span class="sxs-lookup"><span data-stu-id="f167b-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="f167b-127">vlastníka</span><span class="sxs-lookup"><span data-stu-id="f167b-127">Owners</span></span> | <span data-ttu-id="f167b-128">Středníkem oddělený seznam důvěryhodných vlastníků, aby bylo možné dále omezit důvěryhodnost úložiště.</span><span class="sxs-lookup"><span data-stu-id="f167b-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="f167b-129">Platí pouze při použití možnosti `-Repository`.</span><span class="sxs-lookup"><span data-stu-id="f167b-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="f167b-130">Poskytování `-Author` i `-Repository` ve stejnou dobu není podporováno.</span><span class="sxs-lookup"><span data-stu-id="f167b-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="f167b-131">Možnosti pro přidání na základě indexu služby</span><span class="sxs-lookup"><span data-stu-id="f167b-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="f167b-132">_Poznámka_: Tato možnost bude přidávat jenom důvěryhodná úložiště.</span><span class="sxs-lookup"><span data-stu-id="f167b-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="f167b-133">Možnost</span><span class="sxs-lookup"><span data-stu-id="f167b-133">Option</span></span> | <span data-ttu-id="f167b-134">Popis</span><span class="sxs-lookup"><span data-stu-id="f167b-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f167b-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="f167b-135">ServiceIndex</span></span> | <span data-ttu-id="f167b-136">Určuje index služby V3 úložiště, který se má důvěřovat.</span><span class="sxs-lookup"><span data-stu-id="f167b-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="f167b-137">Toto úložiště musí podporovat prostředek pro podpisy úložišť.</span><span class="sxs-lookup"><span data-stu-id="f167b-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="f167b-138">Pokud není zadaný, příkaz bude hledat zdroj balíčku se stejným `-Name` a z něj získá index služby.</span><span class="sxs-lookup"><span data-stu-id="f167b-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="f167b-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="f167b-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="f167b-140">Určuje, jestli by měl být certifikát pro důvěryhodného podepisujícího povolený řetězení k nedůvěryhodnému kořenovému adresáři.</span><span class="sxs-lookup"><span data-stu-id="f167b-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="f167b-141">vlastníka</span><span class="sxs-lookup"><span data-stu-id="f167b-141">Owners</span></span> | <span data-ttu-id="f167b-142">Středníkem oddělený seznam důvěryhodných vlastníků, aby bylo možné dále omezit důvěryhodnost úložiště.</span><span class="sxs-lookup"><span data-stu-id="f167b-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="f167b-143">Možnosti pro přidání na základě informací o certifikátu</span><span class="sxs-lookup"><span data-stu-id="f167b-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="f167b-144">_Poznámka_: Pokud důvěryhodný podpis se zadaným názvem již existuje, bude položka certifikátu přidána k tomuto podepsanému.</span><span class="sxs-lookup"><span data-stu-id="f167b-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="f167b-145">V opačném případě bude vytvořen důvěryhodný autor s položkou certifikátu z daných informací o certifikátu.</span><span class="sxs-lookup"><span data-stu-id="f167b-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="f167b-146">Možnost</span><span class="sxs-lookup"><span data-stu-id="f167b-146">Option</span></span> | <span data-ttu-id="f167b-147">Popis</span><span class="sxs-lookup"><span data-stu-id="f167b-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f167b-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="f167b-148">CertificateFingerprint</span></span> | <span data-ttu-id="f167b-149">Určuje otisky certifikátu certifikátu, pomocí kterého musí být podepsané balíčky podepsané.</span><span class="sxs-lookup"><span data-stu-id="f167b-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="f167b-150">Otisk certifikátu je hodnota hash certifikátu.</span><span class="sxs-lookup"><span data-stu-id="f167b-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="f167b-151">Algoritmus hash použitý pro výpočet tohoto algoritmu hash by měl být určený v možnosti `FingerprintAlgorithm`.</span><span class="sxs-lookup"><span data-stu-id="f167b-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="f167b-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="f167b-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="f167b-153">Určuje algoritmus hash používaný k výpočtu otisku prstu certifikátu.</span><span class="sxs-lookup"><span data-stu-id="f167b-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="f167b-154">Výchozí hodnota je `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="f167b-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="f167b-155">Podporované hodnoty jsou `SHA256`, `SHA384` a `SHA512`</span><span class="sxs-lookup"><span data-stu-id="f167b-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="f167b-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="f167b-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="f167b-157">Určuje, jestli by měl být certifikát pro důvěryhodného podepisujícího povolený řetězení k nedůvěryhodnému kořenovému adresáři.</span><span class="sxs-lookup"><span data-stu-id="f167b-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="f167b-158">Trusted-Signer NuGet – jméno \<název\></span><span class="sxs-lookup"><span data-stu-id="f167b-158">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="f167b-159">Odebere všechny důvěryhodné podepisující osoby, které odpovídají danému názvu.</span><span class="sxs-lookup"><span data-stu-id="f167b-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="f167b-160">\<název synchronizace NuGet-Signer Name\></span><span class="sxs-lookup"><span data-stu-id="f167b-160">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="f167b-161">Vyžádá nejnovější seznam certifikátů používaných v aktuálně důvěryhodném úložišti, aby aktualizoval existující seznam certifikátů v důvěryhodném přihlášení.</span><span class="sxs-lookup"><span data-stu-id="f167b-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="f167b-162">_Poznámka_: Tento gesto odstraní aktuální seznam certifikátů a nahradí je aktuálním seznamem z úložiště.</span><span class="sxs-lookup"><span data-stu-id="f167b-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="f167b-163">Možnosti</span><span class="sxs-lookup"><span data-stu-id="f167b-163">Options</span></span>

| <span data-ttu-id="f167b-164">Možnost</span><span class="sxs-lookup"><span data-stu-id="f167b-164">Option</span></span> | <span data-ttu-id="f167b-165">Popis</span><span class="sxs-lookup"><span data-stu-id="f167b-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f167b-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f167b-166">ConfigFile</span></span> | <span data-ttu-id="f167b-167">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="f167b-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f167b-168">Pokud není zadaný, použije se `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="f167b-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f167b-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f167b-169">ForceEnglishOutput</span></span> | <span data-ttu-id="f167b-170">Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="f167b-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f167b-171">Nápověda</span><span class="sxs-lookup"><span data-stu-id="f167b-171">Help</span></span> | <span data-ttu-id="f167b-172">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="f167b-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="f167b-173">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="f167b-173">Verbosity</span></span> | <span data-ttu-id="f167b-174">Určuje množství podrobností zobrazených ve výstupu: *normální*, *tiché*a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="f167b-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="f167b-175">Příklady</span><span class="sxs-lookup"><span data-stu-id="f167b-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
