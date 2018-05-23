---
title: Podepsané balíčky
description: Požadavky pro podepisování balíčku NuGet.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 72fb1a87c13160c53f632d2ef87a12a4e9bc02a3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/22/2018
---
# <a name="signed-packages"></a><span data-ttu-id="8f315-103">Podepsané balíčky</span><span class="sxs-lookup"><span data-stu-id="8f315-103">Signed packages</span></span>

<span data-ttu-id="8f315-104">*NuGet 4.6.0+ a Visual Studio 2017 verze 15.6 a novější*</span><span class="sxs-lookup"><span data-stu-id="8f315-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="8f315-105">Balíčky NuGet může obsahovat digitální podpis, který poskytuje ochranu proti zmanipulovanou obsah.</span><span class="sxs-lookup"><span data-stu-id="8f315-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="8f315-106">Tento podpis vytváří z certifikát X.509, který také přidá pravosti důkazy skutečné počátek balíčku.</span><span class="sxs-lookup"><span data-stu-id="8f315-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="8f315-107">Podepsané balíčky poskytují nejvyšší ověření začátku do konce.</span><span class="sxs-lookup"><span data-stu-id="8f315-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="8f315-108">Podpisu Autor zaručuje, že balíčku nezměnil od autora podpisu balíčku, bez ohledu z které úložiště nebo co přenosu Metoda doručení balíčku.</span><span class="sxs-lookup"><span data-stu-id="8f315-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="8f315-109">Kromě toho Autor podepsané balíčky poskytnout další ověřovací mechanismus pro publikování kanál nuget.org, protože podpisový certifikát musí být zaregistrovaný předem.</span><span class="sxs-lookup"><span data-stu-id="8f315-109">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="8f315-110">Další informace najdete v tématu [zaregistrovat certifikáty](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="8f315-110">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>

<span data-ttu-id="8f315-111">Podrobnosti o vytváření podepsaného balíčku najdete v tématu [podepisování balíčků](../create-packages/Sign-a-package.md) a [příkaz přihlašovací nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="8f315-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="8f315-112">Podpis balíčku se aktuálně podporuje jenom při použití nuget.exe v systému Windows.</span><span class="sxs-lookup"><span data-stu-id="8f315-112">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="8f315-113">Ověření podepsaný balíčků se aktuálně podporuje jenom při použití nuget.exe nebo Visual Studio v systému Windows.</span><span class="sxs-lookup"><span data-stu-id="8f315-113">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="8f315-114">Požadavky na certifikát</span><span class="sxs-lookup"><span data-stu-id="8f315-114">Certificate requirements</span></span>

<span data-ttu-id="8f315-115">Podpis balíčku vyžaduje certifikát, který je speciálnímu typu certifikátu, který je platný pro podepisování kódu `id-kp-codeSigning` účel [[RFC 5280 části 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="8f315-115">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="8f315-116">Kromě toho musí mít certifikát veřejné délka klíče RSA 2048 bitů nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="8f315-116">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="8f315-117">Získat certifikát pro podpis kódu</span><span class="sxs-lookup"><span data-stu-id="8f315-117">Get a code signing certificate</span></span>

<span data-ttu-id="8f315-118">Platné certifikáty lze získat od veřejné certifikační autority jako:</span><span class="sxs-lookup"><span data-stu-id="8f315-118">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="8f315-119">Symantec</span><span class="sxs-lookup"><span data-stu-id="8f315-119">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="8f315-120">DigiCert</span><span class="sxs-lookup"><span data-stu-id="8f315-120">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="8f315-121">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="8f315-121">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="8f315-122">Globální přihlášení</span><span class="sxs-lookup"><span data-stu-id="8f315-122">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="8f315-123">Comodo</span><span class="sxs-lookup"><span data-stu-id="8f315-123">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="8f315-124">Certum</span><span class="sxs-lookup"><span data-stu-id="8f315-124">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="8f315-125">Úplný seznam certifikačních autorit, které jsou důvěryhodné v systému Windows můžete získat z [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="8f315-125">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="8f315-126">Vytvoření testovacího certifikátu</span><span class="sxs-lookup"><span data-stu-id="8f315-126">Create a test certificate</span></span>

<span data-ttu-id="8f315-127">Pro účely testování můžete svým vydaných certifikátů.</span><span class="sxs-lookup"><span data-stu-id="8f315-127">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="8f315-128">Chcete-li vytvořit certifikát vystavený, použijte [příkazu New-SelfSignedCertificate Powershellu](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="8f315-128">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="8f315-129">Tento příkaz vytvoří testovací certifikát k dispozici v úložišti osobních certifikátů aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="8f315-129">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="8f315-130">Úložiště certifikátů můžete otevřít tak, že spustíte `certmgr.msc` zobrazíte nově vytvořený certifikát.</span><span class="sxs-lookup"><span data-stu-id="8f315-130">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="8f315-131">nuget.org nepřijímá balíčky podepsán svým vydaných certifikátů.</span><span class="sxs-lookup"><span data-stu-id="8f315-131">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="8f315-132">Požadavky na časové razítko</span><span class="sxs-lookup"><span data-stu-id="8f315-132">Timestamp requirements</span></span>

<span data-ttu-id="8f315-133">Podepsané balíčky by měla obsahovat časové razítko RFC 3161 zajistit platnost podpisu nad rámec balíček podepisování doby platnosti certifikátu.</span><span class="sxs-lookup"><span data-stu-id="8f315-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="8f315-134">Musí být platná pro certifikát používaný k podepisování časové razítko `id-kp-timeStamping` účel [[RFC 5280 části 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="8f315-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="8f315-135">Kromě toho musí mít certifikát veřejné délka klíče RSA 2048 bitů nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="8f315-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="8f315-136">Další technické podrobnosti naleznete v [balíček technických specifikací podpis](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (Githubu).</span><span class="sxs-lookup"><span data-stu-id="8f315-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="8f315-137">Požadavky na podpis v nuget.org</span><span class="sxs-lookup"><span data-stu-id="8f315-137">Signature requirements on nuget.org</span></span>

<span data-ttu-id="8f315-138">nuget.org mají další požadavky pro přijetí podepsaného balíčku:</span><span class="sxs-lookup"><span data-stu-id="8f315-138">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="8f315-139">Primární podpis musí být podpisu autora.</span><span class="sxs-lookup"><span data-stu-id="8f315-139">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="8f315-140">Primární podpis musí mít jeden platný časové razítko.</span><span class="sxs-lookup"><span data-stu-id="8f315-140">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="8f315-141">Certifikáty X.509 pro podpis autora a časové razítko podpis:</span><span class="sxs-lookup"><span data-stu-id="8f315-141">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="8f315-142">Musí mít veřejný klíč RSA 2048 bitů nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="8f315-142">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="8f315-143">Musí být v rozsahu období platnosti na aktuální čas UTC během ověřování balíčku na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8f315-143">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="8f315-144">Musí být propojeny s důvěryhodnou kořenovou autoritou, která je důvěryhodná ve výchozím nastavení v systému Windows.</span><span class="sxs-lookup"><span data-stu-id="8f315-144">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="8f315-145">Balíčky s samoobslužné vystavené certifikáty podepsané odmítají.</span><span class="sxs-lookup"><span data-stu-id="8f315-145">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="8f315-146">Musí být platná pro jeho účel:</span><span class="sxs-lookup"><span data-stu-id="8f315-146">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="8f315-147">Autor podpisový certifikát musí být platná pro podepisování kódu.</span><span class="sxs-lookup"><span data-stu-id="8f315-147">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="8f315-148">Certifikát časového razítka musí být platná pro vytvoření časového razítka.</span><span class="sxs-lookup"><span data-stu-id="8f315-148">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="8f315-149">Nesmí být odvolaný při podepisování čas.</span><span class="sxs-lookup"><span data-stu-id="8f315-149">Must not be revoked at signing time.</span></span> <span data-ttu-id="8f315-150">(Nemusí to být knowable během odesílání, takže nuget.org proběhne znovu pravidelně u stav odvolání).</span><span class="sxs-lookup"><span data-stu-id="8f315-150">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="8f315-151">Registrovat certifikát v nuget.org</span><span class="sxs-lookup"><span data-stu-id="8f315-151">Register certificate on nuget.org</span></span>

<span data-ttu-id="8f315-152">Odeslat podepsaný balíček, je nutné nejprve zaregistrovat certifikát s nuget.org. Budete potřebovat certifikát jako `.cer` soubor v binárním formátu DER.</span><span class="sxs-lookup"><span data-stu-id="8f315-152">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="8f315-153">Existující certifikát můžete exportovat do binárního formátu DER pomocí Průvodce exportem certifikátu.</span><span class="sxs-lookup"><span data-stu-id="8f315-153">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Průvodce exportem certifikátu](media/CertificateExportWizard.png)

<span data-ttu-id="8f315-155">Pokročilí uživatelé můžete exportovat certifikát pomocí [příkaz prostředí PowerShell Export certifikátu](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="8f315-155">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="8f315-156">Chcete-li zaregistrovat certifikát s nuget.org, přejděte na `Certificates` části na `Account settings` stránku (nebo organizace nastavení) a vyberte `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="8f315-156">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Certifikáty registrované](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="8f315-158">Jeden uživatel může odeslat, že více certifikátů a stejný certifikát může být registrováno více uživatelů.</span><span class="sxs-lookup"><span data-stu-id="8f315-158">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="8f315-159">Jakmile uživatel, který má certifikát registrován, všechny budoucí balíček odesílání **musí** být podepsány pomocí jednoho z certifikátů.</span><span class="sxs-lookup"><span data-stu-id="8f315-159">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="8f315-160">Uživatelé mohou také odebrat registrovaný certifikát z účtu.</span><span class="sxs-lookup"><span data-stu-id="8f315-160">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="8f315-161">Odebraný certifikát podepsaným tímto certifikátem balíčky nezdaří na odeslání.</span><span class="sxs-lookup"><span data-stu-id="8f315-161">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="8f315-162">Ovlivněné nejsou existující balíčky.</span><span class="sxs-lookup"><span data-stu-id="8f315-162">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="8f315-163">Konfigurace balíčku požadavky na registraci</span><span class="sxs-lookup"><span data-stu-id="8f315-163">Configure package signing requirements</span></span>

<span data-ttu-id="8f315-164">Pokud jste pouze vlastník balíčku, se vyžaduje podepisující osoba.</span><span class="sxs-lookup"><span data-stu-id="8f315-164">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="8f315-165">To znamená všechny certifikáty registrované můžete použít k podepisování vlastních balíčků a odeslání nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8f315-165">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="8f315-166">Pokud balíček obsahuje více vlastníky, ve výchozím nastavení, certifikáty "Žádné" vlastníka můžete použít k podpisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="8f315-166">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="8f315-167">Jako spoluvlastník balíček můžete přepsat "Žádný" sami se sebou nebo jakékoli jiné spoluvlastník být požadované podepisující osoba.</span><span class="sxs-lookup"><span data-stu-id="8f315-167">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="8f315-168">Pokud provedete vlastníka, který nemá zaregistrovaný žádný certifikát, budou mít povolený nepodepsaných balíčků.</span><span class="sxs-lookup"><span data-stu-id="8f315-168">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="8f315-169">Podobně, pokud výchozí možnost "Žádné" pro balíček, kde má jednoho vlastníka certifikát registrován a jiný vlastník nemá zaregistrovaný žádný certifikát, pak nuget.org přijímá podepsaného balíčku podpisem zaregistrován pomocí jednoho z vlastníků nebo Nepodepsaný balíčku (protože jeden z vlastníci není zaregistrovaný žádný certifikát).</span><span class="sxs-lookup"><span data-stu-id="8f315-169">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Konfigurace balíčku podepisující osoby](media/configure-package-signers.png)
