---
title: Příkaz NuGet CLI Trusted-signers
description: Referenční informace k příkazu nuget.exe Trusted-Signer
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9e25f439617a76d30880bea3c10a5d063e681a41
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238150"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="cfb6f-103">příkaz důvěryhodného přihlášení (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cfb6f-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="cfb6f-104">**Platí pro:** &bullet; **podporované verze balíčku:** 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="cfb6f-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="cfb6f-105">Získá nebo nastaví důvěryhodné podepisující osoby na konfiguraci NuGet.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="cfb6f-106">Další informace o využití najdete v tématu [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="cfb6f-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="cfb6f-107">Podrobnosti o tom, jak vypadá nuget.config schéma, najdete v referenční dokumentaci k [konfiguračnímu souboru NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="cfb6f-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="cfb6f-108">Využití</span><span class="sxs-lookup"><span data-stu-id="cfb6f-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="cfb6f-109">Pokud `list|add|remove|sync` není zadán žádný parametr, bude příkaz ve výchozím nastavení nastaven na hodnotu `list` .</span><span class="sxs-lookup"><span data-stu-id="cfb6f-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="cfb6f-110">seznam důvěryhodných podpisů NuGet</span><span class="sxs-lookup"><span data-stu-id="cfb6f-110">nuget trusted-signers list</span></span>

<span data-ttu-id="cfb6f-111">Zobrazí seznam všech důvěryhodných přihlášení v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="cfb6f-112">Tato možnost zahrne všechny certifikáty (s otiskem prstu a otiskem prstu) každého podepsaného.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="cfb6f-113">Pokud předchozí certifikát obsahuje `[U]` , znamená to, že položka certifikátu je `allowUntrustedRoot` nastavená jako `true` .</span><span class="sxs-lookup"><span data-stu-id="cfb6f-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="cfb6f-114">Níže je uvedený příklad výstupu z tohoto příkazu:</span><span class="sxs-lookup"><span data-stu-id="cfb6f-114">Below is an example output from this command:</span></span>

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
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="cfb6f-115">Důvěryhodní přihlášení NuGet – přidat [možnosti]</span><span class="sxs-lookup"><span data-stu-id="cfb6f-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="cfb6f-116">Přidá důvěryhodného podepisujícího se zadaným názvem do konfiguračního souboru. Tato možnost obsahuje různá gesta pro přidání důvěryhodného autora nebo úložiště.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="cfb6f-117">Možnosti pro přidání na základě balíčku</span><span class="sxs-lookup"><span data-stu-id="cfb6f-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="cfb6f-118">kde `<package(s)>` je jeden nebo více `.nupkg` souborů.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

- **`-Author`**

  <span data-ttu-id="cfb6f-119">Určuje, že podpis autora balíčků by měl být důvěryhodný.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-119">Specifies that the author signature of the package(s) should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="cfb6f-120">Určuje, jestli by měl být certifikát pro důvěryhodného podepisujícího povolený řetězení k nedůvěryhodnému kořenovému adresáři.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="cfb6f-121">Středníkem oddělený seznam důvěryhodných vlastníků, aby bylo možné dále omezit důvěryhodnost úložiště.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="cfb6f-122">Platí pouze při použití `-Repository` Možnosti.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="cfb6f-123">Určuje, že signatura úložiště nebo potvrzovací podpisy balíčků by měly být důvěryhodné.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-123">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span>

<span data-ttu-id="cfb6f-124">Poskytování současně `-Author` není `-Repository` podporováno.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="cfb6f-125">Možnosti pro přidání na základě indexu služby</span><span class="sxs-lookup"><span data-stu-id="cfb6f-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="cfb6f-126">_Poznámka_ : Tato možnost bude přidávat jenom důvěryhodná úložiště.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-126">_Note_ : This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="cfb6f-127">Určuje, jestli by měl být certifikát pro důvěryhodného podepisujícího povolený řetězení k nedůvěryhodnému kořenovému adresáři.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="cfb6f-128">Středníkem oddělený seznam důvěryhodných vlastníků, aby bylo možné dále omezit důvěryhodnost úložiště.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="cfb6f-129">Určuje index služby V3 úložiště, který se má důvěřovat.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="cfb6f-130">Toto úložiště musí podporovat prostředek pro podpisy úložišť.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="cfb6f-131">Pokud není zadaný, příkaz bude hledat zdroj balíčku se stejným `-Name` a z něj získá index služby.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="cfb6f-132">Možnosti pro přidání na základě informací o certifikátu</span><span class="sxs-lookup"><span data-stu-id="cfb6f-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="cfb6f-133">_Poznámka_ : Pokud důvěryhodný podpis se zadaným názvem již existuje, bude položka certifikátu přidána k tomuto podepsanému.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-133">_Note_ : If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="cfb6f-134">V opačném případě bude vytvořen důvěryhodný autor s položkou certifikátu z daných informací o certifikátu.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="cfb6f-135">Určuje, jestli by měl být certifikát pro důvěryhodného podepisujícího povolený řetězení k nedůvěryhodnému kořenovému adresáři.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="cfb6f-136">Určuje otisky certifikátu certifikátu, pomocí kterého musí být podepsané balíčky podepsané.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="cfb6f-137">Otisk certifikátu je hodnota hash certifikátu.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="cfb6f-138">Algoritmus hash použitý pro výpočet tohoto algoritmu hash by měl být v `FingerprintAlgorithm` Možnosti určení.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="cfb6f-139">Určuje algoritmus hash používaný k výpočtu otisku prstu certifikátu.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="cfb6f-140">Výchozí hodnota je `SHA256` .</span><span class="sxs-lookup"><span data-stu-id="cfb6f-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="cfb6f-141">Podporované hodnoty jsou `SHA256` `SHA384` a `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="cfb6f-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="cfb6f-142">nedůvěryhodné podepsané – Remove-Name \<name\></span><span class="sxs-lookup"><span data-stu-id="cfb6f-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="cfb6f-143">Odebere všechny důvěryhodné podepisující osoby, které odpovídají danému názvu.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="cfb6f-144">Název synchronizačního podepsaného NuGet-Signer \<name\></span><span class="sxs-lookup"><span data-stu-id="cfb6f-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="cfb6f-145">Vyžádá nejnovější seznam certifikátů používaných v aktuálně důvěryhodném úložišti, aby aktualizoval existující seznam certifikátů v důvěryhodném přihlášení.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="cfb6f-146">_Poznámka_ : Tento gesto odstraní aktuální seznam certifikátů a nahradí je aktuálním seznamem z úložiště.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-146">_Note_ : This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="cfb6f-147">Možnosti</span><span class="sxs-lookup"><span data-stu-id="cfb6f-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="cfb6f-148">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="cfb6f-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cfb6f-149">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="cfb6f-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="cfb6f-150">Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="cfb6f-151">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="cfb6f-152">Jméno důvěryhodného podepisujícího.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="cfb6f-153">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="cfb6f-154">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="cfb6f-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="cfb6f-155">Příklady</span><span class="sxs-lookup"><span data-stu-id="cfb6f-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
