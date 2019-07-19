---
title: Podepsané balíčky
description: Požadavky na podepisování balíčku NuGet
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: e02b2a241008b1b7096f20b351173fd3df7ed172
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317518"
---
# <a name="signed-packages"></a><span data-ttu-id="1f002-103">Podepsané balíčky</span><span class="sxs-lookup"><span data-stu-id="1f002-103">Signed packages</span></span>

<span data-ttu-id="1f002-104">*NuGet 4.6.0 + a Visual Studio 2017 verze 15,6 a novější*</span><span class="sxs-lookup"><span data-stu-id="1f002-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="1f002-105">Balíčky NuGet můžou obsahovat digitální podpis, který poskytuje ochranu proti úmyslnému obsahu.</span><span class="sxs-lookup"><span data-stu-id="1f002-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="1f002-106">Tento podpis je vytvořený z certifikátu X. 509, který taky do skutečného původce balíčku přidá ověření pravosti.</span><span class="sxs-lookup"><span data-stu-id="1f002-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="1f002-107">Podepsané balíčky poskytují nejsilnější kompletní ověřování.</span><span class="sxs-lookup"><span data-stu-id="1f002-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="1f002-108">Existují dva různé typy signatur NuGet:</span><span class="sxs-lookup"><span data-stu-id="1f002-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="1f002-109">**Podpis autora**</span><span class="sxs-lookup"><span data-stu-id="1f002-109">**Author Signature**.</span></span> <span data-ttu-id="1f002-110">Podpis autora zaručuje, že balíček se nezměnil od autora podpisu balíčku bez ohledu na to, ze kterého úložiště nebo jakou metodu transportu balíček doručí.</span><span class="sxs-lookup"><span data-stu-id="1f002-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="1f002-111">Navíc balíčky podepsané autorem poskytují pro kanál publikování nuget.org dodatečný mechanismus ověřování, protože podpisový certifikát musí být zaregistrovaný předem.</span><span class="sxs-lookup"><span data-stu-id="1f002-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="1f002-112">Další informace najdete v tématu [Registrace certifikátů](#signature-requirements-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="1f002-112">For more information, see [Register certificates](#signature-requirements-on-nugetorg).</span></span>
- <span data-ttu-id="1f002-113">**Podpis úložiště**</span><span class="sxs-lookup"><span data-stu-id="1f002-113">**Repository Signature**.</span></span> <span data-ttu-id="1f002-114">Signatury úložiště poskytují záruku integrity pro **všechny** balíčky v úložišti bez ohledu na to, jestli jsou autorem podepsané, nebo ne, a to i v případě, že se tyto balíčky získávají z jiného umístění, než je původní úložiště, ve kterém byly podepsané.</span><span class="sxs-lookup"><span data-stu-id="1f002-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="1f002-115">Podrobnosti o vytvoření balíčku podepsaného autorem najdete v tématu [podepisování balíčků](../create-packages/Sign-a-package.md) a [příkaz NuGet Sign](../reference/cli-reference/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="1f002-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../reference/cli-reference/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="1f002-116">Podepisování balíčků se v současné době podporuje jenom při použití NuGet. exe ve Windows.</span><span class="sxs-lookup"><span data-stu-id="1f002-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="1f002-117">Ověřování podepsaných balíčků se v současné době podporuje jenom při použití NuGet. exe nebo sady Visual Studio ve Windows.</span><span class="sxs-lookup"><span data-stu-id="1f002-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="1f002-118">Požadavky na certifikát</span><span class="sxs-lookup"><span data-stu-id="1f002-118">Certificate requirements</span></span>

<span data-ttu-id="1f002-119">Podepisování balíčků vyžaduje certifikát pro podpis kódu, což je zvláštní typ certifikátu, který je platný pro `id-kp-codeSigning` účely [[RFC 5280 Section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="1f002-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="1f002-120">Certifikát navíc musí mít délku veřejného klíče RSA 2048 bitů nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="1f002-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="1f002-121">Požadavky na časové razítko</span><span class="sxs-lookup"><span data-stu-id="1f002-121">Timestamp requirements</span></span>

<span data-ttu-id="1f002-122">Podepsané balíčky by měly zahrnovat časové razítko RFC 3161 k zajištění platnosti podpisu mimo období platnosti podpisového certifikátu balíčku.</span><span class="sxs-lookup"><span data-stu-id="1f002-122">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="1f002-123">Certifikát použitý k podepsání časového razítka musí být platný pro `id-kp-timeStamping` účely [[RFC 5280 Section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="1f002-123">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="1f002-124">Certifikát navíc musí mít délku veřejného klíče RSA 2048 bitů nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="1f002-124">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="1f002-125">Další technické podrobnosti najdete v [technické specifikaci signatury balíčku](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="1f002-125">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="1f002-126">Požadavky na podpis na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="1f002-126">Signature requirements on NuGet.org</span></span>

<span data-ttu-id="1f002-127">nuget.org má další požadavky na přijetí podepsaného balíčku:</span><span class="sxs-lookup"><span data-stu-id="1f002-127">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="1f002-128">Primární signatura musí být podpis autora.</span><span class="sxs-lookup"><span data-stu-id="1f002-128">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="1f002-129">Primární podpis musí mít jedno platné časové razítko.</span><span class="sxs-lookup"><span data-stu-id="1f002-129">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="1f002-130">Certifikáty X. 509 pro podpis autora i podpis časového razítka:</span><span class="sxs-lookup"><span data-stu-id="1f002-130">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="1f002-131">Musí mít veřejný klíč RSA (2048) nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="1f002-131">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="1f002-132">Musí spadat do období platnosti za aktuální čas UTC v době ověření balíčku v nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1f002-132">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="1f002-133">Musí být zřetězené s důvěryhodnou kořenovou autoritou, která je ve Windows ve výchozím nastavení důvěryhodná.</span><span class="sxs-lookup"><span data-stu-id="1f002-133">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="1f002-134">Balíčky podepsané pomocí certifikátů vystavených svým držitelem jsou odmítnuty.</span><span class="sxs-lookup"><span data-stu-id="1f002-134">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="1f002-135">Musí být platný pro svůj účel:</span><span class="sxs-lookup"><span data-stu-id="1f002-135">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="1f002-136">Podpisový certifikát autora musí být platný pro podepisování kódu.</span><span class="sxs-lookup"><span data-stu-id="1f002-136">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="1f002-137">Certifikát časového razítka musí být platný pro časová razítka.</span><span class="sxs-lookup"><span data-stu-id="1f002-137">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="1f002-138">Nesmí být odvoláno v době podepisování.</span><span class="sxs-lookup"><span data-stu-id="1f002-138">Must not be revoked at signing time.</span></span> <span data-ttu-id="1f002-139">(To nemusí být knowable v době odeslání, takže nuget.org pravidelně znovu kontroluje stav odvolání).</span><span class="sxs-lookup"><span data-stu-id="1f002-139">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>
  
  
## <a name="related-articles"></a><span data-ttu-id="1f002-140">Související články</span><span class="sxs-lookup"><span data-stu-id="1f002-140">Related articles</span></span>

- [<span data-ttu-id="1f002-141">Podepisování balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="1f002-141">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="1f002-142">Správa rozsahu důvěryhodnosti balíčků</span><span class="sxs-lookup"><span data-stu-id="1f002-142">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
