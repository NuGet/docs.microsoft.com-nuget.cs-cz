---
title: NuGet – příkaz Sign CLI
description: Referenční informace k příkazu nuget.exe Sign
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622769"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="f3c86-103">Sign – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f3c86-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="f3c86-104">**Platí pro:** vytváření balíčků &bullet; **podporuje verze:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="f3c86-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="f3c86-105">Podepíše všechny balíčky, které odpovídají prvnímu argumentu s certifikátem.</span><span class="sxs-lookup"><span data-stu-id="f3c86-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="f3c86-106">Certifikát s privátním klíčem lze získat ze souboru nebo z certifikátu nainstalovaného v úložišti certifikátů zadáním názvu předmětu nebo kryptografického otisku.</span><span class="sxs-lookup"><span data-stu-id="f3c86-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

> [!Note]
> <span data-ttu-id="f3c86-107">V rozhraní .NET Core, v mono nebo na platformách jiných než Windows se podepisování balíčků ještě nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="f3c86-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="f3c86-108">Využití</span><span class="sxs-lookup"><span data-stu-id="f3c86-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="f3c86-109">kde `<package(s)>` je jeden nebo více `.nupkg` souborů.</span><span class="sxs-lookup"><span data-stu-id="f3c86-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="f3c86-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="f3c86-110">Options</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="f3c86-111">Určuje otisk SHA-1 certifikátu použitého k hledání místního úložiště certifikátů pro daný certifikát.</span><span class="sxs-lookup"><span data-stu-id="f3c86-111">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span>

- **`-CertificatePassword`**

  <span data-ttu-id="f3c86-112">V případě potřeby Určuje heslo certifikátu.</span><span class="sxs-lookup"><span data-stu-id="f3c86-112">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="f3c86-113">Pokud je certifikát chráněný heslem, ale není k dispozici žádné heslo, příkaz zobrazí výzvu k zadání hesla za běhu, pokud `-NonInteractive` není možnost předána.</span><span class="sxs-lookup"><span data-stu-id="f3c86-113">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the `-NonInteractive` option is passed.</span></span>

- **`-CertificatePath`**

  <span data-ttu-id="f3c86-114">Určuje cestu k souboru certifikátu, který se má použít při podepisování balíčku.</span><span class="sxs-lookup"><span data-stu-id="f3c86-114">Specifies the file path to the certificate to be used in signing the package.</span></span>

- **`-CertificateStoreLocation`**

  <span data-ttu-id="f3c86-115">Určuje název úložiště certifikátů X. 509, které se používá k vyhledání certifikátu.</span><span class="sxs-lookup"><span data-stu-id="f3c86-115">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="f3c86-116">Výchozí hodnota je "CurrentUser", úložiště certifikátů X. 509 používané aktuálním uživatelem.</span><span class="sxs-lookup"><span data-stu-id="f3c86-116">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="f3c86-117">Tato možnost by se měla použít při zadávání certifikátu prostřednictvím `-CertificateSubjectName` nebo `-CertificateFingerprint` možností.</span><span class="sxs-lookup"><span data-stu-id="f3c86-117">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateStoreName`**

  <span data-ttu-id="f3c86-118">Určuje název úložiště certifikátů X. 509, který se použije k vyhledání certifikátu.</span><span class="sxs-lookup"><span data-stu-id="f3c86-118">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="f3c86-119">Výchozí hodnota je my, úložiště certifikátů X. 509 pro osobní certifikáty.</span><span class="sxs-lookup"><span data-stu-id="f3c86-119">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="f3c86-120">Tato možnost by se měla použít při zadávání certifikátu prostřednictvím `-CertificateSubjectName` nebo `-CertificateFingerprint` možností.</span><span class="sxs-lookup"><span data-stu-id="f3c86-120">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateSubjectName`**

  <span data-ttu-id="f3c86-121">Určuje název subjektu certifikátu použitého k hledání místního úložiště certifikátů pro daný certifikát.</span><span class="sxs-lookup"><span data-stu-id="f3c86-121">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="f3c86-122">Hledání je porovnávání řetězců bez rozlišení velkých a malých písmen pomocí zadané hodnoty, která vyhledá všechny certifikáty s názvem subjektu, který tento řetězec obsahuje, bez ohledu na jiné hodnoty předmětu.</span><span class="sxs-lookup"><span data-stu-id="f3c86-122">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="f3c86-123">Úložiště certifikátů lze zadat pomocí `-CertificateStoreName` `-CertificateStoreLocation` možností a.</span><span class="sxs-lookup"><span data-stu-id="f3c86-123">The certificate store can be specified by `-CertificateStoreName` and `-CertificateStoreLocation` options.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="f3c86-124">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="f3c86-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f3c86-125">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="f3c86-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="f3c86-126">Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="f3c86-126">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-HashAlgorithm`**

  <span data-ttu-id="f3c86-127">Algoritmus hash, který se má použít k podepsání balíčku.</span><span class="sxs-lookup"><span data-stu-id="f3c86-127">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="f3c86-128">Výchozí hodnota je SHA256.</span><span class="sxs-lookup"><span data-stu-id="f3c86-128">Defaults to SHA256.</span></span> <span data-ttu-id="f3c86-129">Možné hodnoty jsou SHA256, SHA384 a SHA512.</span><span class="sxs-lookup"><span data-stu-id="f3c86-129">Possible values are SHA256, SHA384, and SHA512.</span></span>

- **`-?|-help`**

  <span data-ttu-id="f3c86-130">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="f3c86-130">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="f3c86-131">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="f3c86-131">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="f3c86-132">Určuje adresář, do kterého se má uložit podepsaný balíček.</span><span class="sxs-lookup"><span data-stu-id="f3c86-132">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="f3c86-133">Ve výchozím nastavení je původní balíček přepsán podepsaným balíčkem.</span><span class="sxs-lookup"><span data-stu-id="f3c86-133">By default the original package is overwritten by the signed package.</span></span>

- **`-Overwrite`**

  <span data-ttu-id="f3c86-134">Přepněte k označení, zda má být aktuální podpis přepsán.</span><span class="sxs-lookup"><span data-stu-id="f3c86-134">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="f3c86-135">Ve výchozím nastavení se příkaz nezdaří, pokud balíček již má podpis.</span><span class="sxs-lookup"><span data-stu-id="f3c86-135">By default the command will fail if the package already has a signature.</span></span>

- **`-Timestamper`**

  <span data-ttu-id="f3c86-136">Adresa URL serveru časového razítka RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="f3c86-136">URL to an RFC 3161 timestamping server.</span></span>

- **`-TimestampHashAlgorithm`**

  <span data-ttu-id="f3c86-137">Algoritmus hash, který má používat server časových razítek RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="f3c86-137">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="f3c86-138">Výchozí hodnota je SHA256.</span><span class="sxs-lookup"><span data-stu-id="f3c86-138">Defaults to SHA256.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="f3c86-139">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="f3c86-139">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="f3c86-140">Příklady</span><span class="sxs-lookup"><span data-stu-id="f3c86-140">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
