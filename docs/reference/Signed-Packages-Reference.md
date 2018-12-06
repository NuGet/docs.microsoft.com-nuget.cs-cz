---
title: Podepsané balíčky
description: Požadavky na podepisování balíčků NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 486bf4032e156168f9b2fef57ccdae0c372b2eff
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977508"
---
# <a name="signed-packages"></a><span data-ttu-id="70700-103">Podepsané balíčky</span><span class="sxs-lookup"><span data-stu-id="70700-103">Signed packages</span></span>

<span data-ttu-id="70700-104">*NuGet 4.6.0+ a sady Visual Studio 2017 verze 15.6 a novější*</span><span class="sxs-lookup"><span data-stu-id="70700-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="70700-105">Balíčky NuGet může obsahovat digitální podpis, který poskytuje ochranu proti zmanipulovanou obsah.</span><span class="sxs-lookup"><span data-stu-id="70700-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="70700-106">Tento podpis je vytvořen z certifikát X.509, který také přidává testování konceptů pravosti skutečné zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="70700-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="70700-107">Podepsané balíčky poskytují nejsilnější ověření začátku do konce.</span><span class="sxs-lookup"><span data-stu-id="70700-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="70700-108">Existují dva různé typy podpisů NuGet:</span><span class="sxs-lookup"><span data-stu-id="70700-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="70700-109">**Vytváření podpis**.</span><span class="sxs-lookup"><span data-stu-id="70700-109">**Author Signature**.</span></span> <span data-ttu-id="70700-110">Podpis autora zaručuje, že balíček nebyl změněn od autora podpisu balíčku, bez ohledu na to, z které úložiště nebo co přenosu metodu doručení balíčku.</span><span class="sxs-lookup"><span data-stu-id="70700-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="70700-111">Kromě toho Autor podepsané balíčky poskytnout další ověřovací mechanismus pro publikování kanál nuget.org, protože podpisový certifikát musí být zaregistrované předem.</span><span class="sxs-lookup"><span data-stu-id="70700-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="70700-112">Další informace najdete v tématu [registrace certifikátů](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="70700-112">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>
- <span data-ttu-id="70700-113">**Podpis úložiště**.</span><span class="sxs-lookup"><span data-stu-id="70700-113">**Repository Signature**.</span></span> <span data-ttu-id="70700-114">Podpisy úložiště poskytuje záruku integrity **všechny** balíčků v úložišti, ať už jsou Autor nebo nemají, i když tyto balíčky jsou získány z jiného umístění než původní úložiště, ve kterém byly podepsané.</span><span class="sxs-lookup"><span data-stu-id="70700-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="70700-115">Podrobnosti o vytvoření podepsaný balíček Autor najdete v tématu [podepisování balíčků](../create-packages/Sign-a-package.md) a [přihlašovací příkaz nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="70700-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="70700-116">Podepisování balíčků aktuálně podporuje jenom při použití nuget.exe ve Windows.</span><span class="sxs-lookup"><span data-stu-id="70700-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="70700-117">Ověření podepsaných balíčků aktuálně podporuje jenom při použití nuget.exe nebo Visual Studio na Windows.</span><span class="sxs-lookup"><span data-stu-id="70700-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="70700-118">Požadavky na certifikát</span><span class="sxs-lookup"><span data-stu-id="70700-118">Certificate requirements</span></span>

<span data-ttu-id="70700-119">Podepisování balíčků vyžaduje certifikát, který je speciální typ certifikátu, který je platný pro podpis kódu `id-kp-codeSigning` účel [[RFC 5280 části 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="70700-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="70700-120">Certifikát musí mít navíc veřejné délka klíče RSA 2048 bitů nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="70700-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="70700-121">Požadavky na časové razítko</span><span class="sxs-lookup"><span data-stu-id="70700-121">Timestamp requirements</span></span>

<span data-ttu-id="70700-122">Podepsané balíčky by měl obsahovat časového razítka RFC 3161 zajistit platnost podpisu mimo období platnosti certifikátu podpisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="70700-122">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="70700-123">Certifikát použitý k podpisu časového razítka musí být platná pro `id-kp-timeStamping` účel [[RFC 5280 části 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="70700-123">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="70700-124">Certifikát musí mít navíc veřejné délka klíče RSA 2048 bitů nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="70700-124">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="70700-125">Další technické podrobnosti najdete v [balíček technické specifikace podpis](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="70700-125">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="70700-126">Požadavky na podpis na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="70700-126">Signature requirements on NuGet.org</span></span>

<span data-ttu-id="70700-127">nuget.org mají další požadavky pro přijetí podepsaný balíček:</span><span class="sxs-lookup"><span data-stu-id="70700-127">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="70700-128">Primární podpis musí být podpis autora.</span><span class="sxs-lookup"><span data-stu-id="70700-128">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="70700-129">Primární podpis musí mít jediné platné časové razítko.</span><span class="sxs-lookup"><span data-stu-id="70700-129">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="70700-130">Certifikátů X.509 pro podpis autora a jeho podpis časového razítka:</span><span class="sxs-lookup"><span data-stu-id="70700-130">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="70700-131">Musí mít veřejný klíč RSA 2048 bitů nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="70700-131">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="70700-132">Musí být v rozsahu období platnosti podle aktuálního času UTC v době ověřování balíčků na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="70700-132">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="70700-133">Musí být propojeny s důvěryhodnou kořenovou autoritou, která je důvěryhodná pro výchozí na Windows.</span><span class="sxs-lookup"><span data-stu-id="70700-133">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="70700-134">Balíčky, které jsou podepsané pomocí samostatně vydané certifikáty byly zamítnuty.</span><span class="sxs-lookup"><span data-stu-id="70700-134">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="70700-135">Musí být platný pro její účel:</span><span class="sxs-lookup"><span data-stu-id="70700-135">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="70700-136">Autor podpisový certifikát musí být platný pro podepisování kódu.</span><span class="sxs-lookup"><span data-stu-id="70700-136">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="70700-137">Certifikát časového razítka musí být platný pro časových razítek.</span><span class="sxs-lookup"><span data-stu-id="70700-137">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="70700-138">Nesmí být odvolaný při podepisování čas.</span><span class="sxs-lookup"><span data-stu-id="70700-138">Must not be revoked at signing time.</span></span> <span data-ttu-id="70700-139">(Toto video asi knowable při odesílání, takže nuget.org proběhne znovu pravidelně u stav odvolání).</span><span class="sxs-lookup"><span data-stu-id="70700-139">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>
  
  
## <a name="related-articles"></a><span data-ttu-id="70700-140">Související články</span><span class="sxs-lookup"><span data-stu-id="70700-140">Related articles</span></span>

- [<span data-ttu-id="70700-141">Podepisují se balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="70700-141">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="70700-142">Instalace podepsaných balíčků</span><span class="sxs-lookup"><span data-stu-id="70700-142">Installing signed packages</span></span>](../consume-packages/installing-signed-packages.md)
