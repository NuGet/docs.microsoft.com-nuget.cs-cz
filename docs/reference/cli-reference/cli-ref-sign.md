---
title: NuGet – příkaz Sign CLI
description: Referenční informace o příkazu NuGet. exe Sign
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328279"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="f7813-103">Příkaz sign (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f7813-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="f7813-104">**Platí pro:** vytváření &bullet; balíčků **podporuje verze:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="f7813-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="f7813-105">Podepíše všechny balíčky, které odpovídají prvnímu argumentu s certifikátem.</span><span class="sxs-lookup"><span data-stu-id="f7813-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="f7813-106">Certifikát s privátním klíčem lze získat ze souboru nebo z certifikátu nainstalovaného v úložišti certifikátů zadáním názvu předmětu nebo kryptografického otisku.</span><span class="sxs-lookup"><span data-stu-id="f7813-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="f7813-107">V rozhraní .NET Core, v mono nebo na platformách jiných než Windows se podepisování balíčků ještě nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="f7813-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="f7813-108">Použití</span><span class="sxs-lookup"><span data-stu-id="f7813-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="f7813-109">kde `<package(s)>` je jeden nebo více `.nupkg` souborů.</span><span class="sxs-lookup"><span data-stu-id="f7813-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="f7813-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="f7813-110">Options</span></span>

| <span data-ttu-id="f7813-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="f7813-111">Option</span></span> | <span data-ttu-id="f7813-112">Popis</span><span class="sxs-lookup"><span data-stu-id="f7813-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f7813-113">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="f7813-113">CertificateFingerprint</span></span> | <span data-ttu-id="f7813-114">Určuje otisk SHA-1 certifikátu použitého k hledání místního úložiště certifikátů pro daný certifikát.</span><span class="sxs-lookup"><span data-stu-id="f7813-114">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="f7813-115">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="f7813-115">CertificatePassword</span></span> | <span data-ttu-id="f7813-116">V případě potřeby Určuje heslo certifikátu.</span><span class="sxs-lookup"><span data-stu-id="f7813-116">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="f7813-117">Pokud je certifikát chráněný heslem, ale není k dispozici žádné heslo, příkaz zobrazí výzvu k zadání hesla v době běhu, pokud není předána možnost-neinteraktivní.</span><span class="sxs-lookup"><span data-stu-id="f7813-117">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="f7813-118">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="f7813-118">CertificatePath</span></span> | <span data-ttu-id="f7813-119">Určuje cestu k souboru certifikátu, který se má použít při podepisování balíčku.</span><span class="sxs-lookup"><span data-stu-id="f7813-119">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="f7813-120">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="f7813-120">CertificateStoreLocation</span></span> | <span data-ttu-id="f7813-121">Určuje název úložiště certifikátů X. 509, které se používá k vyhledání certifikátu.</span><span class="sxs-lookup"><span data-stu-id="f7813-121">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="f7813-122">Výchozí hodnota je "CurrentUser", úložiště certifikátů X. 509 používané aktuálním uživatelem.</span><span class="sxs-lookup"><span data-stu-id="f7813-122">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="f7813-123">Tato možnost by se měla použít při zadávání certifikátu prostřednictvím možností-CertificateSubjectName nebo-CertificateFingerprint.</span><span class="sxs-lookup"><span data-stu-id="f7813-123">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="f7813-124">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="f7813-124">CertificateStoreName</span></span> | <span data-ttu-id="f7813-125">Určuje název úložiště certifikátů X. 509, který se použije k vyhledání certifikátu.</span><span class="sxs-lookup"><span data-stu-id="f7813-125">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="f7813-126">Výchozí hodnota je my, úložiště certifikátů X. 509 pro osobní certifikáty.</span><span class="sxs-lookup"><span data-stu-id="f7813-126">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="f7813-127">Tato možnost by se měla použít při zadávání certifikátu prostřednictvím možností-CertificateSubjectName nebo-CertificateFingerprint.</span><span class="sxs-lookup"><span data-stu-id="f7813-127">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="f7813-128">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="f7813-128">CertificateSubjectName</span></span> | <span data-ttu-id="f7813-129">Určuje název subjektu certifikátu použitého k hledání místního úložiště certifikátů pro daný certifikát.</span><span class="sxs-lookup"><span data-stu-id="f7813-129">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="f7813-130">Hledání je porovnávání řetězců bez rozlišení velkých a malých písmen pomocí zadané hodnoty, která vyhledá všechny certifikáty s názvem subjektu, který tento řetězec obsahuje, bez ohledu na jiné hodnoty předmětu.</span><span class="sxs-lookup"><span data-stu-id="f7813-130">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="f7813-131">Úložiště certifikátů lze zadat pomocí možností-CertificateStoreName a-CertificateStoreLocation.</span><span class="sxs-lookup"><span data-stu-id="f7813-131">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="f7813-132">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f7813-132">ConfigFile</span></span> | <span data-ttu-id="f7813-133">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="f7813-133">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f7813-134">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="f7813-134">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f7813-135">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f7813-135">ForceEnglishOutput</span></span> | <span data-ttu-id="f7813-136">Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="f7813-136">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f7813-137">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="f7813-137">HashAlgorithm</span></span> | <span data-ttu-id="f7813-138">Algoritmus hash, který se má použít k podepsání balíčku.</span><span class="sxs-lookup"><span data-stu-id="f7813-138">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="f7813-139">Výchozí hodnota je SHA256.</span><span class="sxs-lookup"><span data-stu-id="f7813-139">Defaults to SHA256.</span></span> |
| <span data-ttu-id="f7813-140">Help</span><span class="sxs-lookup"><span data-stu-id="f7813-140">Help</span></span> | <span data-ttu-id="f7813-141">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="f7813-141">Displays help information for the command.</span></span> |
| <span data-ttu-id="f7813-142">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f7813-142">NonInteractive</span></span> | <span data-ttu-id="f7813-143">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="f7813-143">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f7813-144">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="f7813-144">OutputDirectory</span></span> | <span data-ttu-id="f7813-145">Určuje adresář, do kterého se má uložit podepsaný balíček.</span><span class="sxs-lookup"><span data-stu-id="f7813-145">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="f7813-146">Ve výchozím nastavení je původní balíček přepsán podepsaným balíčkem.</span><span class="sxs-lookup"><span data-stu-id="f7813-146">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="f7813-147">Přepsat</span><span class="sxs-lookup"><span data-stu-id="f7813-147">Overwrite</span></span> | <span data-ttu-id="f7813-148">Přepněte k označení, zda má být aktuální podpis přepsán.</span><span class="sxs-lookup"><span data-stu-id="f7813-148">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="f7813-149">Ve výchozím nastavení se příkaz nezdaří, pokud balíček již má podpis.</span><span class="sxs-lookup"><span data-stu-id="f7813-149">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="f7813-150">Časové razítko</span><span class="sxs-lookup"><span data-stu-id="f7813-150">Timestamper</span></span> | <span data-ttu-id="f7813-151">Adresa URL serveru časového razítka RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="f7813-151">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="f7813-152">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="f7813-152">TimestampHashAlgorithm</span></span> | <span data-ttu-id="f7813-153">Algoritmus hash, který má používat server časových razítek RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="f7813-153">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="f7813-154">Výchozí hodnota je SHA256.</span><span class="sxs-lookup"><span data-stu-id="f7813-154">Defaults to SHA256.</span></span> |
| <span data-ttu-id="f7813-155">Verbosity</span><span class="sxs-lookup"><span data-stu-id="f7813-155">Verbosity</span></span> | <span data-ttu-id="f7813-156">Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="f7813-156">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="f7813-157">Příklady</span><span class="sxs-lookup"><span data-stu-id="f7813-157">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```