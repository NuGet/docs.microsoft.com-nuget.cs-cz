---
title: Podepsané balíčky
description: Požadavky na podepisování balíčků NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c36db9486ad787f19430c75fc38a2e9dd8ba6e37
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550418"
---
# <a name="signed-packages"></a><span data-ttu-id="8d0e3-103">Podepsané balíčky</span><span class="sxs-lookup"><span data-stu-id="8d0e3-103">Signed packages</span></span>

<span data-ttu-id="8d0e3-104">*NuGet 4.6.0+ a sady Visual Studio 2017 verze 15.6 a novější*</span><span class="sxs-lookup"><span data-stu-id="8d0e3-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="8d0e3-105">Balíčky NuGet může obsahovat digitální podpis, který poskytuje ochranu proti zmanipulovanou obsah.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="8d0e3-106">Tento podpis je vytvořen z certifikát X.509, který také přidává testování konceptů pravosti skutečné zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="8d0e3-107">Podepsané balíčky poskytují nejsilnější ověření začátku do konce.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="8d0e3-108">Existují dva různé typy podpisů NuGet:</span><span class="sxs-lookup"><span data-stu-id="8d0e3-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="8d0e3-109">**Vytváření podpis**.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-109">**Author Signature**.</span></span> <span data-ttu-id="8d0e3-110">Podpis autora zaručuje, že balíček nebyl změněn od autora podpisu balíčku, bez ohledu na to, z které úložiště nebo co přenosu metodu doručení balíčku.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="8d0e3-111">Kromě toho Autor podepsané balíčky poskytnout další ověřovací mechanismus pro publikování kanál nuget.org, protože podpisový certifikát musí být zaregistrované předem.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="8d0e3-112">Další informace najdete v tématu [registrace certifikátů](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="8d0e3-112">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>
- <span data-ttu-id="8d0e3-113">**Podpis úložiště**.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-113">**Repository Signature**.</span></span> <span data-ttu-id="8d0e3-114">Podpisy úložiště poskytuje záruku integrity **všechny** balíčků v úložišti, ať už jsou Autor nebo nemají, i když tyto balíčky jsou získány z jiného umístění než původní úložiště, ve kterém byly podepsané.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="8d0e3-115">Podrobnosti o vytvoření podepsaný balíček Autor najdete v tématu [podepisování balíčků](../create-packages/Sign-a-package.md) a [přihlašovací příkaz nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="8d0e3-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="8d0e3-116">Podepisování balíčků aktuálně podporuje jenom při použití nuget.exe ve Windows.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="8d0e3-117">Ověření podepsaných balíčků aktuálně podporuje jenom při použití nuget.exe nebo Visual Studio na Windows.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="8d0e3-118">Požadavky na certifikát</span><span class="sxs-lookup"><span data-stu-id="8d0e3-118">Certificate requirements</span></span>

<span data-ttu-id="8d0e3-119">Podepisování balíčků vyžaduje certifikát, který je speciální typ certifikátu, který je platný pro podpis kódu `id-kp-codeSigning` účel [[RFC 5280 části 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="8d0e3-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="8d0e3-120">Certifikát musí mít navíc veřejné délka klíče RSA 2048 bitů nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="8d0e3-121">Získat certifikát pro podpis kódu</span><span class="sxs-lookup"><span data-stu-id="8d0e3-121">Get a code signing certificate</span></span>

<span data-ttu-id="8d0e3-122">Platné certifikáty lze získat od veřejné certifikační autority, jako jsou:</span><span class="sxs-lookup"><span data-stu-id="8d0e3-122">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="8d0e3-123">Symantec</span><span class="sxs-lookup"><span data-stu-id="8d0e3-123">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="8d0e3-124">DigiCert</span><span class="sxs-lookup"><span data-stu-id="8d0e3-124">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="8d0e3-125">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="8d0e3-125">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="8d0e3-126">Globální přihlašování</span><span class="sxs-lookup"><span data-stu-id="8d0e3-126">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="8d0e3-127">Comodo</span><span class="sxs-lookup"><span data-stu-id="8d0e3-127">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="8d0e3-128">Certum</span><span class="sxs-lookup"><span data-stu-id="8d0e3-128">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="8d0e3-129">Úplný seznam certifikačních autorit důvěryhodná pro Windows můžou pocházet od [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="8d0e3-129">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="8d0e3-130">Vytvoření testovacího certifikátu</span><span class="sxs-lookup"><span data-stu-id="8d0e3-130">Create a test certificate</span></span>

<span data-ttu-id="8d0e3-131">Pro účely testování můžete použít samostatně vydané certifikáty.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-131">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="8d0e3-132">Chcete-li vytvořit certifikát vystavený, použijte [příkazu Powershellu New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="8d0e3-132">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

```ps
New-SelfSignedCertificate -Subject "CN=NuGet Test Developer, OU=Use for testing purposes ONLY" `
                          -FriendlyName "NuGetTestDeveloper" `
                          -Type CodeSigning `
                          -KeyUsage DigitalSignature `
                          -KeyLength 2048 `
                          -KeyAlgorithm RSA `
                          -HashAlgorithm SHA256 `
                          -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                          -CertStoreLocation "Cert:\CurrentUser\My" 
```

<span data-ttu-id="8d0e3-133">Tento příkaz vytvoří testovací certifikát k dispozici v úložišti osobních certifikátů aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-133">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="8d0e3-134">Můžete otevřít úložiště certifikátů spuštěním `certmgr.msc` zobrazíte nově vytvořeného certifikátu.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-134">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="8d0e3-135">nuget.org nepřijímá žádné balíčky podepsané pomocí samostatně vydané certifikáty.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-135">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="8d0e3-136">Požadavky na časové razítko</span><span class="sxs-lookup"><span data-stu-id="8d0e3-136">Timestamp requirements</span></span>

<span data-ttu-id="8d0e3-137">Podepsané balíčky by měl obsahovat časového razítka RFC 3161 zajistit platnost podpisu mimo období platnosti certifikátu podpisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-137">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="8d0e3-138">Certifikát použitý k podpisu časového razítka musí být platná pro `id-kp-timeStamping` účel [[RFC 5280 části 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="8d0e3-138">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="8d0e3-139">Certifikát musí mít navíc veřejné délka klíče RSA 2048 bitů nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-139">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="8d0e3-140">Další technické podrobnosti najdete v [balíček technické specifikace podpis](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="8d0e3-140">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="8d0e3-141">Požadavky na podpis na nuget.org</span><span class="sxs-lookup"><span data-stu-id="8d0e3-141">Signature requirements on nuget.org</span></span>

<span data-ttu-id="8d0e3-142">nuget.org mají další požadavky pro přijetí podepsaný balíček:</span><span class="sxs-lookup"><span data-stu-id="8d0e3-142">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="8d0e3-143">Primární podpis musí být podpis autora.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-143">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="8d0e3-144">Primární podpis musí mít jediné platné časové razítko.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-144">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="8d0e3-145">Certifikátů X.509 pro podpis autora a jeho podpis časového razítka:</span><span class="sxs-lookup"><span data-stu-id="8d0e3-145">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="8d0e3-146">Musí mít veřejný klíč RSA 2048 bitů nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-146">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="8d0e3-147">Musí být v rozsahu období platnosti podle aktuálního času UTC v době ověřování balíčků na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-147">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="8d0e3-148">Musí být propojeny s důvěryhodnou kořenovou autoritou, která je důvěryhodná pro výchozí na Windows.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-148">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="8d0e3-149">Balíčky, které jsou podepsané pomocí samostatně vydané certifikáty byly zamítnuty.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-149">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="8d0e3-150">Musí být platný pro její účel:</span><span class="sxs-lookup"><span data-stu-id="8d0e3-150">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="8d0e3-151">Autor podpisový certifikát musí být platný pro podepisování kódu.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-151">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="8d0e3-152">Certifikát časového razítka musí být platný pro časových razítek.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-152">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="8d0e3-153">Nesmí být odvolaný při podepisování čas.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-153">Must not be revoked at signing time.</span></span> <span data-ttu-id="8d0e3-154">(Toto video asi knowable při odesílání, takže nuget.org proběhne znovu pravidelně u stav odvolání).</span><span class="sxs-lookup"><span data-stu-id="8d0e3-154">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="8d0e3-155">Zaregistrovat certifikát na nuget.org</span><span class="sxs-lookup"><span data-stu-id="8d0e3-155">Register certificate on nuget.org</span></span>

<span data-ttu-id="8d0e3-156">Odeslat podepsaný balíček, musíte nejprve zaregistrovat certifikát s nuget.org. Budete potřebovat certifikát jako `.cer` soubor ve formátu binární kódování DER.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-156">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="8d0e3-157">Existující certifikát, který můžete exportovat do formátu binární kódování DER s použitím Průvodce exportem certifikátu.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-157">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Průvodce exportem certifikátu](media/CertificateExportWizard.png)

<span data-ttu-id="8d0e3-159">Pokročilí uživatelé mohou exportovat certifikát pomocí [příkazu Powershellu Export certifikátu](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="8d0e3-159">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="8d0e3-160">Chcete-li zaregistrovat certifikát s nuget.org, přejděte na `Certificates` části na `Account settings` stránky (nebo stránku nastavení organizace) a vyberte `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-160">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Certifikáty registrované](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="8d0e3-162">Jeden uživatel může odeslat svoji, že více certifikátů a stejný certifikát může být registrováno více uživatelů.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-162">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="8d0e3-163">Jakmile uživatel certifikát zaregistrovaný, všechny příspěvky budoucí balíček **musí** být podepsány pomocí jednoho z certifikátů.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-163">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="8d0e3-164">Uživatelé mohou také odebírat registrovaný certifikát z účtu.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-164">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="8d0e3-165">Po odebrání certifikát v odesílání selhat balíčky podepsaným tímto certifikátem.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-165">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="8d0e3-166">Nemají vliv na existující balíčky.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-166">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="8d0e3-167">Konfigurovat požadavky na podepisování balíčku</span><span class="sxs-lookup"><span data-stu-id="8d0e3-167">Configure package signing requirements</span></span>

<span data-ttu-id="8d0e3-168">Pokud jste jediným vlastníkem balíček, jsou požadované podepisující osoba.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-168">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="8d0e3-169">To znamená slouží všechny certifikáty registrované k podepisování balíčků a odesílání do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-169">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="8d0e3-170">Pokud balíček obsahuje více vlastníkům, ve výchozím nastavení, "Libovolné" vlastník certifikáty lze použít k podpisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-170">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="8d0e3-171">Jako spoluvlastníka balíček můžete přepsat "Žádný" sami se sebou nebo jakékoli jiné spoluvlastník bude požadované podepisující osoba.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-171">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="8d0e3-172">Pokud provedete vlastníka, který nemá žádné certifikát zaregistrovaný, budou mít povolený balíčky bez znaménka.</span><span class="sxs-lookup"><span data-stu-id="8d0e3-172">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="8d0e3-173">Podobně, pokud výchozí "Libovolné" výběru balíčky, kde má certifikát zaregistrovaný jednoho vlastníka a dalšího vlastníka nemá žádné certifikát zaregistrovaný, pak nuget.org přijímá podepsaný balíček s podpisem registrovaných jednoho ze svých vlastníků nebo bez znaménka balíček (protože jeden z vlastníků nemá žádné certifikát zaregistrovaný).</span><span class="sxs-lookup"><span data-stu-id="8d0e3-173">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Konfigurace podepsaných balíčků](media/configure-package-signers.png)
