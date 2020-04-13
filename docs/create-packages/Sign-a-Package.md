---
title: Podepisování balíčků NuGet
description: Vysvětluje, jak lze podepsané balíčky použít k povolení ověření integrity obsahu.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 00fe1d5fa81132b5d6826203a0d26e56aa8d4755
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429001"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="3ea20-103">Podepisování balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="3ea20-103">Signing NuGet Packages</span></span>

<span data-ttu-id="3ea20-104">Podepsané balíčky umožňují kontrolu ověření integrity obsahu, která poskytuje ochranu proti manipulaci s obsahem.</span><span class="sxs-lookup"><span data-stu-id="3ea20-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="3ea20-105">Podpis balíčku slouží také jako jediný zdroj pravdy o skutečném původu balíčku a posiluje pravost balíčku pro spotřebitele.</span><span class="sxs-lookup"><span data-stu-id="3ea20-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="3ea20-106">Tato příručka předpokládá, že jste již [vytvořili balíček](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="3ea20-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="3ea20-107">Získání certifikátu pro podepisování kódu</span><span class="sxs-lookup"><span data-stu-id="3ea20-107">Get a code signing certificate</span></span>

<span data-ttu-id="3ea20-108">Platné certifikáty lze získat od veřejné certifikační autority, jako jsou [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)atd. Úplný seznam certifikačních úřadů důvěryhodných systémem [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners)Windows lze získat z aplikace .</span><span class="sxs-lookup"><span data-stu-id="3ea20-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="3ea20-109">Pro účely testování můžete použít certifikáty s vlastním vydáním.</span><span class="sxs-lookup"><span data-stu-id="3ea20-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="3ea20-110">Balíčky podepsané pomocí certifikátů vydaných samostatně však nejsou NuGet.org akceptovány. Další informace o [vytvoření testovacího certifikátu](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="3ea20-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="3ea20-111">Export souboru certifikátu</span><span class="sxs-lookup"><span data-stu-id="3ea20-111">Export the certificate file</span></span>

* <span data-ttu-id="3ea20-112">Existující certifikát můžete exportovat do binárního formátu DER pomocí Průvodce exportem certifikátu.</span><span class="sxs-lookup"><span data-stu-id="3ea20-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Průvodce exportem certifikátu](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="3ea20-114">Certifikát můžete také exportovat pomocí [příkazu Export-Certificate PowerShell](/powershell/module/pkiclient/export-certificate).</span><span class="sxs-lookup"><span data-stu-id="3ea20-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="3ea20-115">Podepište balíček</span><span class="sxs-lookup"><span data-stu-id="3ea20-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="3ea20-116">Vyžaduje nuget.exe 4.6.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="3ea20-116">Requires nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="3ea20-117">Dotnet.exe podpora je již brzy - [#7939](https://github.com/NuGet/Home/issues/7939)</span><span class="sxs-lookup"><span data-stu-id="3ea20-117">dotnet.exe support is coming soon - [#7939](https://github.com/NuGet/Home/issues/7939)</span></span>

<span data-ttu-id="3ea20-118">Podepište balíček pomocí [nugetového znaku](../reference/cli-reference/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="3ea20-118">Sign the package using [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="3ea20-119">Poskytovatel certifikátu často také poskytuje adresu URL serveru časových razítek, kterou můžete použít pro výše uvedenou povinnou `Timestamper` argumentaci.</span><span class="sxs-lookup"><span data-stu-id="3ea20-119">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="3ea20-120">Obraťte se na dokumentaci a/nebo podporu této adresy URL služby od svého poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="3ea20-120">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="3ea20-121">Můžete použít certifikát dostupný v úložišti certifikátů nebo certifikát ze souboru.</span><span class="sxs-lookup"><span data-stu-id="3ea20-121">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="3ea20-122">Viz odkaz na CLI pro [znaménko nuget](../reference/cli-reference/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="3ea20-122">See CLI reference for [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span></span>
* <span data-ttu-id="3ea20-123">Podepsané balíčky by měly obsahovat časové razítko, abyste měli jistotu, že podpis zůstane platný i po vypršení platnosti podpisového certifikátu.</span><span class="sxs-lookup"><span data-stu-id="3ea20-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="3ea20-124">Jinak bude operace znaku produkovat [upozornění](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="3ea20-124">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="3ea20-125">Můžete zobrazit podrobnosti o podpisu daného balíčku pomocí [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="3ea20-125">You can see the signature details of a given package using [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="3ea20-126">Registrace certifikátu na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="3ea20-126">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="3ea20-127">Chcete-li publikovat podepsaný balíček, musíte nejprve zaregistrovat certifikát u NuGet.org. Certifikát potřebujete jako `.cer` soubor v binárním formátu DER.</span><span class="sxs-lookup"><span data-stu-id="3ea20-127">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="3ea20-128">[Přihlaste](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se k NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="3ea20-128">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="3ea20-129">Přejděte `Account settings` na `Manage Organization` **>** `Edit Organziation` (nebo pokud chcete certifikát zaregistrovat pomocí účtu organizace).</span><span class="sxs-lookup"><span data-stu-id="3ea20-129">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="3ea20-130">Rozbalte `Certificates` oddíl `Register new`a vyberte .</span><span class="sxs-lookup"><span data-stu-id="3ea20-130">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="3ea20-131">Procházejte a vyberte soubor certficate, který byl exportován dříve.</span><span class="sxs-lookup"><span data-stu-id="3ea20-131">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="3ea20-132">![Registrované certifikáty](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="3ea20-132">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="3ea20-133">**Poznámka**</span><span class="sxs-lookup"><span data-stu-id="3ea20-133">**Note**</span></span>
* <span data-ttu-id="3ea20-134">Jeden uživatel může odeslat více certifikátů a stejný certifikát může být registrován více uživateli.</span><span class="sxs-lookup"><span data-stu-id="3ea20-134">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="3ea20-135">Jakmile má uživatel certifikát registrovaný, **musí** být všechny budoucí odeslání balíčku podepsány jedním z certifikátů.</span><span class="sxs-lookup"><span data-stu-id="3ea20-135">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="3ea20-136">Viz [Správa požadavků na podepisování pro váš balíček na NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="3ea20-136">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="3ea20-137">Uživatelé mohou také odebrat registrovaný certifikát z účtu.</span><span class="sxs-lookup"><span data-stu-id="3ea20-137">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="3ea20-138">Po odebrání certifikátu se při odeslání nezdaří nové balíčky podepsané tímto certifikátem.</span><span class="sxs-lookup"><span data-stu-id="3ea20-138">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="3ea20-139">Existující balíčky nejsou ovlivněny.</span><span class="sxs-lookup"><span data-stu-id="3ea20-139">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="3ea20-140">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="3ea20-140">Publish the package</span></span>

<span data-ttu-id="3ea20-141">Nyní jste připraveni publikovat balíček NuGet.org. Viz [Publikování balíčků](../nuget-org/Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="3ea20-141">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="3ea20-142">Vytvoření testovacího certifikátu</span><span class="sxs-lookup"><span data-stu-id="3ea20-142">Create a test certificate</span></span>

<span data-ttu-id="3ea20-143">Pro účely testování můžete použít certifikáty s vlastním vydáním.</span><span class="sxs-lookup"><span data-stu-id="3ea20-143">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="3ea20-144">Chcete-li vytvořit certifikát s vlastním vydáním, použijte [příkaz New-SelfSignedCertificate PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="3ea20-144">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="3ea20-145">Tento příkaz vytvoří testovací certifikát, který je k dispozici v úložišti osobních certifikátů aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="3ea20-145">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="3ea20-146">Úložiště certifikátů můžete otevřít `certmgr.msc` spuštěním a zobrazit nově vytvořený certifikát.</span><span class="sxs-lookup"><span data-stu-id="3ea20-146">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="3ea20-147">NuGet.org nepřijímá balíčky podepsané certifikáty vydanými samostatně.</span><span class="sxs-lookup"><span data-stu-id="3ea20-147">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="3ea20-148">Správa požadavků na podepisování pro váš balíček na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="3ea20-148">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="3ea20-149">[Přihlaste](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se k NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="3ea20-149">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="3ea20-150">Přejít `Manage Packages`  
    ![na Konfigurovat podepisující balíky](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="3ea20-150">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="3ea20-151">Pokud jste jediným vlastníkem balíčku, jste povinným podepi NuGet.orgsujícím, tj.</span><span class="sxs-lookup"><span data-stu-id="3ea20-151">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="3ea20-152">Pokud balíček má více vlastníků, ve výchozím nastavení "Všechny" certifikáty vlastníka lze použít k podpisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="3ea20-152">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="3ea20-153">Jako spoluvlastník balíčku můžete přepsat "Any" se sebou nebo jiným spoluvlastníkem, abyste byli povinni podepisovat.</span><span class="sxs-lookup"><span data-stu-id="3ea20-153">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="3ea20-154">Pokud vytvoříte vlastníka, který nemá žádný certifikát registrovaný, budou povoleny nepodepsané balíčky.</span><span class="sxs-lookup"><span data-stu-id="3ea20-154">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="3ea20-155">Podobně pokud je pro balíček vybrána výchozí možnost "Any", kde má jeden vlastník certifikát registrovaný a jiný vlastník nemá žádný certifikát registrovaný, přijme NuGet.org podepsaný balíček s podpisem registrovaným jedním z jeho vlastníků nebo nepodepsaný balíček (protože jeden z vlastníků nemá žádný certifikát registrovaný).</span><span class="sxs-lookup"><span data-stu-id="3ea20-155">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="3ea20-156">Související články</span><span class="sxs-lookup"><span data-stu-id="3ea20-156">Related articles</span></span>

- [<span data-ttu-id="3ea20-157">Správa rozsahu důvěryhodnosti balíčků</span><span class="sxs-lookup"><span data-stu-id="3ea20-157">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="3ea20-158">Odkaz na podepsané balíčky</span><span class="sxs-lookup"><span data-stu-id="3ea20-158">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
